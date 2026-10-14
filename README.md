# 大直高中雲端工作秘書（公開瀏覽版）

這是公開免登入的靜態網站。首頁為 `index.html`，行事曆資料為 `data.json`。原本指向不存在的 `/api/secure` 的 rewrite 已移除。

## Vercel 部署
1. 在 Vercel → Add New → Project 選擇 GitHub `kevin750521/dazhi-work-secretary`。
2. Framework Preset 選 **Other**，Root Directory 保持 **./**，Build Command 留空，Output Directory 留空（使用預設）。
3. 按 Deploy。若專案已存在，進入該專案 → Deployments → Redeploy 最新 commit。
4. 用無痕視窗測試首頁、月曆及資料載入。

## 重要限制
- GitHub 公開及網站免登入代表任何人都可能讀取 `data.json`。**禁止放入學生個資、內部行政資訊、帳密或金鑰**；上線前務必審核資料。
- 目前 `data.json` 是匯出快照，尚未連線 Google Sheets 自動同步。
- 日期必須是明確單日才可列入月曆；日期區間、待公告資料留在待確認清單。
- 正式網址以 Vercel 實際部署結果為準；若未出現在 Vercel Git 匯入清單，檢查 GitHub App 儲存庫存取權。
