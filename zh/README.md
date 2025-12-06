# 關於 NodeX

<p align="right"><a href="https://docs.node-x.xyz/en">English</a></p>

NodeX 是一個全球化的分散式算力網路，將伺服器、PC、GPU、手機、IoT 與邊緣設備統一虛擬化為可供 AI 直接呼叫的可信執行層（Real-World Execution Layer）。

NodeX 的核心目標，是為 AI 建構一種新的基礎設施形態：\
**AI 的身體（AI Body）——讓 AI 能夠在真實世界執行任務、調度資源、產生行動。**

換句話說：\
雲讓 AI 擁有「超級大腦」，NodeX 讓 AI 擁有「可協調的分散式身體」。

NodeX 透過可驗證計算、設備能力抽象、身份體系與市場機制，使 AI 代理能以安全、標準化、可信的方式呼叫世界各地的真實設備能力，從而完成超越雲端運算範疇的任務。

## **1. 為什麼需要 NodeX（以及 AI 為什麼需要「身體」）**

現代 AI（包括 LLM、Agent、SLM）具備強大的認知能力，但缺乏以下能力：

* 無法自主管理真實設備
* 無法訪問攝像頭、感測器、邊緣節點
* 無法在用戶側設備上執行任務
* 無法驗證外部節點是否真實完成工作
* 無法從真實世界獲取複雜的 I/O 輸入
* 無法像一個自主系統那樣對環境施加影響

這意味著：\
AI 擁有「智能」，但缺乏「行動力」。

DeepMind 的 _Virtual Agent Economies_ 明確指出：\
AI 代理經濟無法成立，除非 AI 能以可信方式與現實世界的執行層相連接。

NodeX 提供的正是這個執行層，即：\
**AI 的身體（AI Body Layer）**——\
由全球設備構成、可被 AI 呼叫、可驗證、可定價、可管理。

***

## **2. NodeX 如何構建 AI 的身體**

AI 的身體不是機器人，也不是單一設備，而是一個多層結構：

> AI 身體 = 設備（Devices） + 能力（Capabilities） + 調度（Execution） + 可信（Verification）

NodeX 在這四個維度上提供了一套完整體系：

***

**2.1 設備層（Devices）**

任何設備都可以接入 NodeX：

* 伺服器
* 家用 PC
* GPU
* 手機
* IoT / 感測器
* 家用 NAS
* 攝像頭
* 邊緣運算節點

這些設備共同構成 AI 的「肌肉與器官」。

***

**2.2 能力層（Capabilities）**

每台設備會將自身能力註冊到 NodeX 的 **能力註冊中心（Capability Registry）**：

例如：

* `compute.run`
* `shell.exec`
* `camera.capture`
* `sensor.read`
* `model.inference`
* `storage.write`

這些能力構成 AI 的「手、眼與神經系統」。

NodeX 提供統一的任務呼叫介面：

<pre class="language-http"><code class="lang-http"><strong> POST /v1/jobs {
</strong>  capability,
  input,
  selector
}
</code></pre>

AI 或開發者可以直接呼叫全球設備來執行任務。\
這就是 AI 的「動作系統」。

**2.4 可信層（Verification）**

AI 要使用設備，必須先能信任設備。\
NodeX 提供：

* **ProofX** → 設備真實性與基礎能力驗證
* **PoRW** → 防造假的真實工作證明
* **RP / AP** → 信譽與貢獻積分
* **MID** → 持久的機器身份

這一層就像是 AI 的「免疫系統」和「安全系統」。

## **3. 為什麼 AI 的身體對未來至關重要**

AI 不再只是一個模型，而將成為**自主行動的系統（Autonomous Systems）**。\
這類系統需要：

* 感知
* 執行
* 回饋
* 協作
* 可信度
* 任務完成的可稽核性

而這些，都依賴一個分散式的「身體」。

NodeX 所提供的「身體層」，解決了以下痛點（對應 VAE）：\
暫時無法在 Lark 文件外展示此內容

AI 的訓練在雲端進行，\
AI 的行動則在 NodeX 上發生。

***

## **4. NodeX 六層架構（AI Body Stack）**

NodeX 的系統架構，可以視為一個分散式的「AI 身體協議棧」：

1. 設備層（Device Layer）
2. 能力層（Capability Layer）
3. 可信層（Trust Layer）
4. 執行層（Execution Layer）
5. 結算層（Settlement Layer）
6. 應用層（Application Layer）

NodeX 不是一個單一工具，而是一套可組合的底層執行網路。

***

## **5. NodeX 核心產品如何服務 AI 身體**

**NodeHub**\
構建「身體」的入口（設備管理、能力映射、驗證與調度）。

**TaskPad**\
任務生態系統（AI 身體所使用的「動作腳本」由社群貢獻）。

**C2C Marketplace**\
為 AI 的身體提供可定價、可驗證的資源供給。

## **6. NodeX 的價值主張（AI 的身體 = 新時代基礎設施）**

NodeX 解決了未來 10 年 AI 系統最關鍵的痛點：

* AI 不再侷限於雲端推理
* AI 可以第一次在真實世界執行任務
* AI 可以呼叫真實設備並為所用資源支付費用
* 設備可以透過貢獻能力獲得收入
* 專案 / Agent 可以拿到可驗證的執行結果

NodeX 讓世界第一次可以：\
把全球的設備組織成 AI 的「身體」，\
形成一張**可編排、可驗證的執行網路**。

***

## **7. 願景**

NodeX 的長期目標：

* 打造 AI 的全球執行層（AI Body Layer）
* 為設備建立可持續的收入體系（Machine Income Layer）
* 為 AI 代理經濟提供可信的基礎設施
* 建立一個開放、透明、可驗證的算力與能力網路

未來的 AI 不只需要算力，\
更需要一具**可信、安全、可擴展的身體**。

NodeX，正在構建這個身體。
