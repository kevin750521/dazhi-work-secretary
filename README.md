# 大直高中私人工作秘書｜部署套件

本專案的 HTML 和資料快照位於 `private/`，不以靜態檔案公開；所有頁面及 `/data.json` 均經過伺服器端登入驗證。未設定環境變數時，網站回傳 503 而非公開資料。

## 部署
1. GitHub 建立 **Private** repository `dazhi-work-secretary`，上傳本套件檔案（包含 `api/secure.js`、`private/`、`vercel.json`）。
2. Vercel 新增 Project → Import Git Repository，選取該私人 repo，Framework Preset 選 Other。
3. 在 Vercel Project Settings → Environment Variables 設定 `ADMIN_USERNAME`、`ADMIN_PASSWORD`（強密碼）、`SESSION_SECRET`（至少 32 位元組隨機值）。切勿寫進 GitHub 檔案。將環境變數套用 Production、Preview，重新部署。
4. 部署後以未登入的無痕視窗測試 `/`、`/data.json` 皆不可直接讀取，登入後才能讀取；登出 `/logout` 後應再次被擋下。
5. 在既有 sports-hub 新增指向實際 Vercel 網址的入口；網址以 Vercel 成功部署後提供為準。

## 安全限制
- 此為單一管理者密碼登入的初版；沒有多使用者、雙因素驗證、密碼重設、IP 限速與登入嘗試限制。正式存放學生個資前應改用成熟的身份供應商（如 Google Workspace SSO）與角色權限、稽核日誌。
- 請勿將敏感個資放入原始碼或 Git 歷史紀錄；私人 GitHub 不等於網站訪客自動受保護。
- 本套件資料為先前匯出的快照，**尚未完成 Google Sheets 自動同步**。

## 同步規劃
由受權的後端排程讀取 Google Sheets，解析確定日期、驗證 ISO 單日日期，日期區間或未公告移至 `pending`；僅將去識別化的允許欄位同步至私有儲存空間，避免在 Git 提交敏感資料。同步應記錄最後成功時間、來源版本、錯誤訊息與去重鍵。建議先採每 3 小時一次。
