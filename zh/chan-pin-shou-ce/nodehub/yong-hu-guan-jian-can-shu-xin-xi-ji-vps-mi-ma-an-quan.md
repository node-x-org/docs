# 用戶關鍵參數資訊及 VPS 密碼安全

## 關鍵參數資訊安全

### 1. 參數存儲安全性

您在 NodeHub 上填寫的參數會經過伺服器加密存儲，僅用戶本人可以查看自己的明文參數。即使其他人獲得了數據，也只能看到密文，無法破解或查看具體內容。

#### 為何需要保存參數？

保存部分數據有助於未來的操作流程，具體目的是：

* **部署失敗重試**：當部署失敗時，用戶可直接使用已保存的參數進行快速重試，提升操作效率。
* **問題追溯**：保存參數有助於分析和排查部署過程中可能遇到的問題。
* **便捷再次部署**：在用戶進行二次部署時，無需重複填寫相同的參數，從而節省時間和精力。

### 2. 更多安全功能

我們計劃在未來推出以下安全功能：

* **一鍵清除參數功能**：用戶可以隨時清除已保存的參數，保證數據隱私不被泄露。
* **二次驗證機制**：針對關鍵數據，我們將引入雙重加密等二次驗證手段，用戶需設置安全密鑰或啟用雙重身份驗證（2FA）才能獲取相關數據，進一步保障數據安全。

### 3. 安全提示

儘管我們已採取多項安全措施來保護用戶的參數和數據，但我們仍然強烈建議：

* 所有涉及私鑰的項目應使用新的錢包。
* 妥善保管自己的帳號密碼，並避免在多個平台或環境中重複使用相同的密碼。

**安全提示總結**：數據安全是我們首要關注的問題。NodeHub 在加密存儲、雙重身份驗證等方面持續改進，並且始終建議用戶采取最嚴格的安全措施來保護自己的帳戶和私鑰。

