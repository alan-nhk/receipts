# 收據上載系統 (receipts)

個人收據自動整理網站。上載收據相片或 PDF，AI 會自動辨識內容並寫入 Google 試算表。

**網址：** https://alan-nhk.github.io/receipts/

---

## 運作方式

```
瀏覽器（本頁，GitHub Pages 靜態網頁）
        │  POST JSON (text/plain，避開 CORS preflight)
        ▼
Google Apps Script 網頁應用（後端，執行身份＝帳戶持有人）
        ├─ 檔案存入 Google Drive 指定資料夾
        ├─ 呼叫 Gemini 2.5 Flash 辨識收據（支援一張圖內多張收據）
        └─ 寫入試算表「自動整合」分頁（含重複偵測）
```

- 本頁只是前端介面（純 HTML / CSS / JS），**不含任何 API key**。
- Gemini API key 存放於 Apps Script 後端的 `程式碼.gs`，瀏覽者無法取得。
- 後端程式碼在本機維護，不在這個 repo（此 repo 只放前端）。

## 檔案

| 檔案 | 用途 |
|---|---|
| `index.html` | 整個上載介面（單一檔案，無外部依賴） |

## 維護

改完 `index.html` 後重新部署即可：

```bash
python3 ~/.workbuddy/skills/github-web-publish/scripts/gh_api_deploy_static.py receipts "<這個資料夾的絕對路徑>"
```

## 注意

- 網址為公開網址。請勿公開分享給不信任的人。
- 上載檔案上限約 15MB。
