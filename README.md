# 南一三上 1–6 課生字聽寫輪盤

這是一個適合 iPad Safari 使用的靜態網頁聽寫遊戲，不需要伺服器或資料庫。

## 目前內容

- 初始詞庫：84 個不重複語詞。
- 覆蓋：南一三上第 1–6 課共 90 個目標生字。
- 組詞原則：語詞中的字都限定在「三上 1–6 課目標生字」或提供的既有累積生字中。
- 輪盤不顯示答案，只顯示神祕符號；抽題後用瀏覽器語音朗讀。
- 可標記「答對／再練習」，錯題標記及學習紀錄只保存在該裝置的瀏覽器 localStorage。
- 教師／家長可新增語詞、匯入／匯出 `words.json`。
- GitHub Pages 上首次載入後，Service Worker 會快取主要檔案，便於 iPad 再次開啟。

## 檔案

- `index.html`：主程式，可直接使用；內含初始詞庫備援。
- `words.json`：GitHub Pages 使用的可更新詞庫。
- `sw.js`：離線快取。
- `word_audit.csv`：初始詞庫檢核表，列出課次、複習生字、搭配字及是否出現詞庫限制外文字。

## 部署到 GitHub Pages

1. 在 GitHub 建立一個新的 repository，例如 `nani-dictation-wheel`。
2. 把 `index.html`、`words.json`、`sw.js` 上傳到 repository 根目錄。`README.md` 與 `word_audit.csv` 可一併上傳。
3. 進入 repository 的 **Settings → Pages**。
4. 在 **Build and deployment** 的 **Source** 選 **Deploy from a branch**。
5. Branch 選 `main`，資料夾選 `/(root)`，按 **Save**。
6. 發布後網址通常會是：
   `https://你的GitHub帳號.github.io/nani-dictation-wheel/`
7. 在 iPad 用 Safari 開啟網址；可用 Safari 的「分享 → 加入主畫面」建立像 App 一樣的入口。

GitHub 官方目前支援從指定 branch 的根目錄或 `/docs` 目錄發布 Pages；本專案不需要額外 build，因此用 `main` + `/(root)` 最簡單。

## 日後擴充詞庫

### 方法 A：直接改 GitHub 的 words.json
每筆資料格式：

```json
{
  "id": "W001",
  "word": "泥巴",
  "lessons": [1],
  "targets": ["泥"],
  "note": ""
}
```

`lessons` 可以同時放多課，例如「負責」可標成 `[3, 6]`。

### 方法 B：在網頁內新增後匯出
1. 展開「教師／家長工具」。
2. 新增語詞。
3. 按「匯出 words.json」。
4. 將匯出的檔案取代 GitHub repository 中的 `words.json`。

這樣其他 iPad 或電腦重新開啟網站後，也能讀到更新後的詞庫。

## 語音注意事項

程式優先選擇 `zh-TW` 語音。iPad Safari 若因系統限制沒有自動朗讀，可直接按「再聽一次」；此按鈕由使用者觸控觸發，通常最穩定。

## 隱私

學生姓名、答題結果與錯題紀錄不會上傳到 GitHub；它們只儲存在目前裝置瀏覽器的 localStorage。請不要把任何個人資料寫進 `words.json` 或 repository。
