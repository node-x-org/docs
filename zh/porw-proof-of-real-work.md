# PoRW（Proof of Real Work）

## 真實工作量證明機制（Version 1.0）

***

### 1. 概述（Overview）

PoRW（Proof of Real Work）是 NodeX 為全球分布式設備設計的 **可驗證執行機制**，用於證明某個設備確實執行了真實任務，並將貢獻轉化為可計量的工作量，用於：

* 節點貢獻度計算
* 網絡調度優先級
* 激勵分配（Reward Distribution）
* 設備信譽體系（MID）
* AI Body Layer 的可信執行系統

PoRW 的目標非常明確：\
**讓每一次真實的設備工作都可被證明，讓每一份貢獻都被公平激勵。**

PoRW 解決了 Web3、DePIN、AI 代理經濟長期存在的核心問題：

* 很難驗證設備是否真實執行任務
* 難以區分真實節點與虛假節點（Sybil Attack）
* 黑盒系統輸出難以驗證
* 任務執行不可審計
* 無法形成可信的獎勵閉環

***

### 2. 核心理念：三維混合驗證（Tri-Dimensional Verification）

PoRW 摒棄傳統單一驗證方式（如只驗證結果、只驗算力申報、只看在線率等），\
而是基於 NodeX 對設備的 **腳本控制能力 + 分布式任務能力 + 市場博弈機制**，\
構建了 **三維、異構、互補的驗證體系**：

#### 2.1 物理與邏輯對撞（Correlation）

**適用：** 挖礦 / 黑盒類任務

通過以下手段進行交叉驗證：

* 本地腳本上報 → 日誌、進程、資源佔用
* 鏈上或第三方 API 數據 → 實際收益 / Share / 區塊高度

邏輯對撞可檢測：

* 本地偽造日誌
* 後台脫離平台獨立運行
* “假工作、真收益”型欺詐

***

#### 2.2 概率性冗餘共識（Probabilistic Redundancy）

**適用：** AI 推理 / 計算類任務

核心思想：\
對同一任務，隨機調度多個同類設備執行，並進行結果比對。

技術機制：

* 固定執行環境（Seeds、參數一致）
* 多節點執行同一任務
* 哈希 / pHash / CLIP Score 等比對
* 少數服從多數（Byzantine-style consensus）

能夠防止：

* 外包執行
* 跳過計算
* 會話偽造
* 隨機性欺騙

***

#### 2.3 社會化仲裁（Social Arbitration）

**適用：** C2C 算力交易、直接交付業務

核心手段：

* 買賣雙方的經濟博弈
* 信譽質押與懲罰
* 自動腳本 + 用戶舉報的共同驗證

可識別：

* 虛假在線
* 性能虛標
* 作弊規避工作

***

### 3. PoRW 總體架構（Architecture）

PoRW 引擎位於：

調度層（Coordinator Layer）\
↕\
PoRW 引擎\
↕\
結算層（Settlement Layer）

輸出統一的 **UoC（Unit of Compute，算力貢獻單位）**。

***

#### 3.1 角色定義

* **Worker（設備 / 節點）：** 執行任務並生成 PoRW 數據
* **Dispatcher（調度器）：** 下發任務與腳本
* **Verifier（驗證器）：** 執行對撞、比對、日誌分析
* **Reporter（監督者）：** 來自 C2C 市場的用戶或高信譽節點

## 4. 模組化驗證模型（Module-Level Implementation）

PoRW 拆分為四類任務模型，對應四類現實常見任務：

### 模組 A：流量型驗證（Traffic-Based Verification）

**適用範圍**：RPC、API、網路服務、負載均衡節點

**機制**：金絲雀請求 + 流量鏡像

* 隨機混入帶有已知結果的測試請求
* Worker 無法區分真實請求 vs 測試請求
* 若測試失敗 → 整個時間窗口工作量無效

**評分公式**：

Score = (Requests × Success\_Rate) − (Penalty × Latency\_Factor)

***

### 模組 B：結果映射型驗證（Result-Based Verification）

**適用範圍**：PoW 挖礦、CDN、黑盒節點、測試網節點

**機制**：內查外核

* **內部腳本日誌指紋（Local Script）**：用於追蹤節點內部操作行為
* **外部鏈上資料 / API（Oracle Data）**：驗證節點輸出與外部真實資料一致性

**判斷邏輯**：

| Local\_Log | Chain\_Data | 結論          |
| ---------- | ----------- | ----------- |
| 正常         | 正常          | 有效貢獻        |
| 正常         | 無收益         | 配置錯誤 / 偽造日誌 |
| 停止         | 有收益         | 脫離平台挂机（無效）  |

### 模組 C：計算生成型驗證（Compute-Based Verification）

**適用範圍**：AI 推理、圖像生成、視頻處理、數值計算

**機制**：概率性冗餘共識

* 同一任務發給 3 台同構設備
* 結果比對（Hash / pHash / CLIP Score）
* 少數服從多數
* 作弊節點扣分、降信譽

**增強機制**：

* 圖片逆向識別（反推輸入 → 判斷真實性）

***

### 模組 D：C2C 交易型驗證（SLA-Based Verification）

**適用範圍**：算力租賃、任務交付、點對點執行

**機制**：社會化仲裁

* 信譽質押
* SLA 監控
* 買家舉報 → 系統回溯腳本記錄
* 違規 → 扣押金 / 降信譽

## 5. 統一結算模型（Unified Settlement Model）

所有任務的 PoRW 最終轉換為統一的貢獻度：

PoRW\_Final = Base\_Work × Quality\_Index × Reputation\_Factor

* **Base\_Work**：請求數、計算量、任務耗時等
* **Quality\_Index**：成功率、延遲、性能波動
* **Reputation\_Factor**：基於 MID 的信譽評分（0.0–1.5）

> 信譽成為最重要的乘數因子

***

## 6. 反作弊體系（Anti-Cheat System）

PoRW 提供五層防護：

1. 隨機挑戰（抗預計算）
2. 多點比對（抗偽造、抗跳算）
3. 時間+性能曲線（抗外包執行）
4. 環境指紋（抗模擬設備）
5. 信譽衰減（降低作弊經濟回報）

***

## 7. 與其他驗證技術（ZKP / TEE / Oracle / MPC）的互補關係

PoRW 並不試圖替代現有驗證技術，而是與其共同構成 **可信執行棧（Trusted Execution Stack）**。

### 7.1 與 ZKP（零知識證明）互補

**ZKP 適合**：

* 確定性計算
* 數學計算
* 小規模任務可證明性

**PoRW 適合**：

* 長時任務
* 黑盒系統
* AI 推理（不可完全用 ZKP 驗證）

> ZKP 是結果證明，PoRW 是過程證明

***

### 7.2 與 TEE（可信執行環境）互補

**TEE 適合**：

* 保護執行環境
* 防篡改

**PoRW 適合**：

* 大規模分布式節點
* 非可信硬體（IoT、家用 PC、VPS）
* 驗證執行真實性

> TEE 是可信空間，PoRW 是可信行為

***

### 7.3 與外部預言機（Oracle）互補

* **Oracle** 提供「外部真實資料」
* **PoRW** 提供「內部執行真實性」

二者結合可驗證：

* 本地日誌 vs 鏈上資料
* 任務輸入 vs 結果映射

> Oracle 證明「結果真實」，PoRW 證明「過程真實」

***

## 8. PoRW 的意義（Why PoRW Matters）

PoRW 讓 NodeX 成為：

* 可驗證執行平台
* 可信設備網路
* AI Body Layer 的底座
* 機器經濟的基礎設施

**一句話總結 PoRW**：

> 沒有 PoRW，AI 無法信任設備；\
> 沒有 PoRW，設備無法獲得可信收益

***

## 9. PoRW 路線圖（Public Roadmap）

**Phase 1：基礎驗證（當前）**

* 腳本下發、日誌回傳
* 設備指紋與信譽庫

**Phase 2：接入層驗證**

* 模組 A/B 全面上線
* 礦工節點對撞驗證

**Phase 3：計算共識層**

* 模組 C 大規模部署
* 分布式任務比對引擎

**Phase 4：自動化結算**

* PoRW 完整積分模型上線
* 支持上鏈或 TEE 可信結算

***

## 10. 最終目標（End State）

PoRW 帶來一個全新的機器協作時代：

* 設備獲得真實可持續收益
* AI 代理擁有可信執行層
* 全網貢獻透明、可審計、不可作假
* NodeX 成為全球最大的可信機器執行網路
