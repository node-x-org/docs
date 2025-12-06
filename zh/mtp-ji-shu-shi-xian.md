# MTP 技術實現

## 1.前言

NodeX 正在構建機器經濟的「信任與執行層」，\
讓每一台真實設備都能被驗證、被證明、被激勵。

當前階段的核心任務：\
打通 MTP 與 x402，讓每一筆機器支付都基於真實且可驗證的計算行為

## 2.系統總覽

&#x20;系統層級

| 層級               | 功能定義                                | 對應模組          |
| ---------------- | ----------------------------------- | ------------- |
| Compute Layer    | <p>真實算力節點（CPU / GPU / Edge）<br></p> | NodeHub       |
| Trust Layer      | <p>身份驗證 + 工作證明</p><p></p>           | ProofX + PoRW |
| Payment Layer    | <p>智能體支付協議<br></p>                  | x402          |
| Settlement Layer | <p>多方結算 / 記帳分潤<br></p>              | x403          |

Flow:

```
Device → ProofX → PoRW → MTP Registry → x402 Payment → x403 Settlement
```

一句話邏輯：

先驗證（MTP），再支付（x402）

## 3.設備身份與指紋

ProofX 會為每一台接入 NodeHub 的設備生成加密指紋，並在鏈上錨定其真實性。

**技術機制：**

1️⃣ **設備指紋（Device Fingerprint）**

* 收集 CPU ID、MAC 位址、磁碟 UUID、TPM 雜湊值、BIOS 簽名。
* 使用 SHA3 與 BLAKE3 進行雜湊處理。
* 加入隨機數（nonce），防止重放攻擊。

2️⃣ **節點憑證（Node Certificate）**

* 由 NodeHub CA（憑證簽發機構）簽發短期憑證（有效期 7–30 天）。
* 以 `certificate_id + proofx_id` 的形式進行存儲。

3️⃣ **鏈上驗證（On-chain Verification）**

* 執行 `verify(ProofX_ID, Signature)` 以確認設備與憑證的真實性。

Output Example:

```
{
  "proofx_id": "0xabc123",
  "certificate_id": "cert_2025_11_01",
  "signature": "0x4a5b..."
}
```

## 4.真實工作證明

PoRW 用來驗證每台設備所執行的工作是真實且有效的，並生成可重複驗證的「工作證明」。

**工作流程：**

1️⃣ **記錄任務指標**\
記錄 CPU、記憶體、IO、網路等資源使用情況。

2️⃣ **計算工作雜湊（Work Hash）**\
計算公式：\
`WorkHash = SHA3(TaskID + Timestamp + DeviceHash + ResourceUsage)`

3️⃣ **生成 PoRW 記錄**\
基於上述資訊生成對應的 PoRW 工作記錄。

4️⃣ **上鏈提交**\
將 PoRW 記錄提交至 MTP 註冊表（MTP Registry）。

```
{
  "task_id": "task_0G_41289",
  "work_hash": "0xdef456",
  "validator_signature": "0xa43b..."
}
```

## 5.本地簽名與驗證

* 通過 secp256k1 / BLS 進行本地簽名
* 內嵌運行於 NodeHub 客戶端中
* 負責 ProofX 身份與 PoRW 驗證
* 將已簽名的證明推送至中繼（Relay），再上傳至 MTP 註冊表

## 6. 信任註冊合約

```
pragma solidity ^0.8.0;

contract MTPRegistry {
    struct ProofRecord {
        bytes32 proofx_id;
        bytes32 work_hash;
        bytes32 x402_invoice_id;
        uint256 timestamp;
        address device;
    }

    mapping(bytes32 => ProofRecord) public records;

    event ProofVerified(bytes32 indexed proofx_id, bytes32 indexed work_hash);
    event ProofSubmitted(bytes32 indexed proofx_id, bytes32 indexed work_hash, address device);

    function submitProof(bytes32 _proofx_id, bytes32 _work_hash, bytes32 _invoice) external {
        records[_proofx_id] = ProofRecord(_proofx_id, _work_hash, _invoice, block.timestamp, msg.sender);
        emit ProofSubmitted(_proofx_id, _work_hash, msg.sender);
    }

    function verifyMTP(bytes32 _proofx_id, bytes32 _work_hash) external view returns (bool) {
        return records[_proofx_id].work_hash == _work_hash;
    }
}
```

## 7.支付整合層

x402 定義「怎麼付」，MTP 定義「為什麼值得付、該付給誰」，\
而 NodeHub 是兩者之間的執行橋樑，讓每一筆付款都建立在真實計算之上。

Bridge Contract:

```
function verifyAndPay(bytes32 proofx_id, bytes32 work_hash) external {
    bool valid = IMTPRegistry(mtp).verifyMTP(proofx_id, work_hash);
    require(valid, "Invalid MTP proof");
    IX402Payment(x402).releasePayment(proofx_id, work_hash);
}
```

Combined Flow:

```
Task Executed → Proof Generated (MTP)
→ On-chain Verification → x402 Payment Released
→ x403 Settlement Finalized
```

## 8.中繼層同步邏輯

* 映射 `ProofX_ID` 與 `x402_invoice_id` 之間的對應關係
* 向註冊表提交證明與計費資訊
* 在驗證完成後，呼叫 x402 支付介面

Relay Log Example:

```
{
  "task_id": "task_elixir_023",
  "proofx_id": "0xabc...",
  "work_hash": "0xdef...",
  "x402_invoice_id": "inv_2025_001",
  "status": "verified"
}
```

## **9. SDK 初始化示例**

Go SDK

```
client := mtp.NewClient("relay.nodehub.global")
proofxID, _ := client.RegisterDevice()
proof := client.GeneratePoRW("task_0G_41289", proofxID)
txHash, _ := client.SubmitProof(proof)
```

Rust SDK

```
let mut client = Client::new("relay.nodehub.global");
let proofx_id = client.register_device()?;
let proof = TaskProof::new("task_story_989", &proofx_id);
let tx_hash = client.submit_proof(proof)?;
```

Python SDK

```
client = MTPClient(endpoint="relay.nodehub.global")
proofx_id = client.register_device()
proof = client.generate_porw(task_id="task_elixir_023", proofx_id=proofx_id)
tx_hash = client.submit_proof(proof)
```

## **10.  開發者接入清單**

**運行環境：**

* 安裝 NodeHub v3.2 及以上版本
* 從開發者控制台獲取 API 金鑰
* 設定接入端點：`relay.nodehub.global`

**集成步驟：**\
1️⃣ 註冊 ProofX → 獲取 `proofx_id`\
2️⃣ 執行任務 → 生成 `porw_record`\
3️⃣ 提交證明 → 上傳至 MTP 註冊表\
4️⃣ 若驗證通過，x402 將自動觸發支付

**Outputs / 輸出結果：**

* `proofx_id`
* `work_hash`
* `x402_invoice_id`
* `verified_status`

## **11.** 當前開發路線圖

| 階段 | 時間       | 模組                                | 輸出                     |
| -- | -------- | --------------------------------- | ---------------------- |
| P1 | Week 1–2 | ProofX ↔ Invoice 映射規則             | schema.json            |
| P2 | Week 3   | MTP Registry + x402 Bridge 合約MTP  | <p>Solidity 模組<br></p> |
| P3 | Week 4   | Relay Billing API聯調               | <p>REST 介面<br></p>     |
| P4 | Week 5   | 与 X Layer 聯測 Joint                | 測試報告 T                 |
| P5 | Week 6   | NodeHub v3.3 Beta 上線              | Beta發佈說明               |

## **12. 生態項目集成模板**

| 項目        | 角色                  | 集成價值                          |
| --------- | ------------------- | ----------------------------- |
| 0G        | AI Alignment Nodes  | <p>可信算力日誌與支付自動觸發<br></p>      |
| Boundless | GPU Mining Pools    | <p>防作弊 + 可驗證收益分配<br></p>      |
| Nexus     | Global Compute Grid | <p>MTP 驗證作為全球信任地圖<br>MTP </p> |

合作方集成步驟

1️⃣ 接入 NodeHub SDK\
2️⃣ 綁定 ProofX 與 x402 發票號\
3️⃣ 啟用自動支付觸發\
4️⃣ 啟用「Verified by MTP」徽章

## 13.安全機制：

* 硬體綁定的 ProofX 指紋
* 基於隨機數的防重放機制
* 雙重簽名（設備 + 中繼）
* 本地驗證 —— 無中心化依賴

## **14.战略愿景**

x402 解決了支付，MTP 解決了信任，NodeHub 讓一切真正落地。

## 總結一句：

NodeX = 機器支付的可信執行層

NodeHub = Proof → Pay 的真實執行入口。
