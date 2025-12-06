---
layout:
  width: default
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# 項目背景

<p align="right"><a href="https://docs.node-x.xyz/en/about-nodex/project-background">English</a></p>

現代 AI 正從「模型時代」邁向「自主代理（Agent）時代」，\
但支撐代理在真實世界中**執行、驗證與協作**的底層技術基建仍然缺失。

DeepMind《Virtual Agent Economies (VAE)》明確指出當前系統存在三大結構性技術缺口：

1. **缺乏可信設備身份層**\
   AI 無法鑑別外部設備的真實性、穩定性或可靠性，也無法在不可信環境中安全操作。
2. **缺乏可驗證執行層（Verifiable Execution）**\
   現有系統無法證明遠端算力任務或設備行為是否真實發生，無法抵禦偽造工作量。
3. **缺乏跨異構設備的能力抽象層（Capability Abstraction）**\
   AI 無法理解、選擇或編排真實世界中不同設備的能力，更無法在規模上加以調用。

與此同時，全球算力環境呈現高度碎片化：

* 數據中心利用率 < 50%
* GPU 實際利用率僅 20–30%
* 500 億＋設備（PC、手機、IoT、邊緣設備）具備巨大但尚未被有效利用的算力與感測能力
* 缺乏統一的 API、調度層、信任機制與設備能力註冊體系

從分散式系統的角度來看，缺失的基礎層其實非常清晰：\
👉 **AI 缺乏一個連接雲端與真實世界的、可編程且可驗證的執行協議層。**

NodeX Masterplan 將這一缺失定義為 **AI 身體層（AI Body Layer）**，其架構由四個核心技術子層組成：

* **設備層（Device Layer）**：全球異構硬體
* **能力層（Capability Layer）**：設備能力的標準化抽象
* **執行層（Execution Layer）**：任務路由、分配與調度
* **驗證層（Verification Layer）**：由 ProofX、PoRW、MID 構成的可信體系

這四層共同構成了 AI 從「能思考」走向「能行動」的根本技術基礎，\
為代理在真實世界中執行任務提供可信環境。

NodeX 的使命，就是構建這一層，通過：

* 將異構設備接入統一的全球設備圖
* 以標準能力介面對外暴露真實設備能力
* 透過分散式調度與執行引擎完成任務執行
* 以加密證明驗證真實工作量
* 建立機器身份與長期信譽體系

從根本上填補當前 AI 與現實世界之間**缺失的協議層**。

**一句話總結：**\
行業缺少一個讓 AI 能在真實世界中執行任務的「可驗證協議層」，\
而 NodeX 正在實現這個協議。
