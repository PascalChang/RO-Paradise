# 🏰 RO 掉落物品查詢系統

一個基於 Google 試算表和幻想廳 RO 資料庫的仙境傳說裝備掉落查詢網站，支援多類別裝備和怪物資料搜尋、篩選和排序功能。

## ✨ 功能特色

- **多類別支援**: 武器、頭具、衣服、披肩、鞋子、盾、飾品
- **怪物查詢**: 支援怪物名稱、種族、屬性、體型等查詢
- **智能搜尋**: 支援物品名稱、掉落魔物、職業限制等關鍵字搜尋
- **進階篩選**: 按職業限制、等級限制、裝備類別、怪物種族、體型篩選
- **排序功能**: 按名稱、等級限制、類別、怪物等級、HP等排序
- **分頁顯示**: 支援自訂每頁顯示數量
- **響應式設計**: 支援手機、平板、桌面裝置
- **即時統計**: 顯示總物品數、怪物數、符合條件數等統計資訊

## 📊 資料統計

- **總物品數**: 61 個
- **武器**: 42 個
- **頭具**: 1 個
- **衣服**: 8 個
- **披肩**: 2 個
- **鞋子**: 3 個
- **盾**: 4 個
- **飾品**: 1 個

- **總怪物數**: 約 1000+ 個
- **等級範圍**: 1-250 級
- **一般怪物**: 包含各種等級的普通怪物
- **特殊怪物**: 包含高等級和特殊怪物

## 📚 資料來源

### 裝備資料
所有裝備資料均來自以下 Google 試算表：

- [掉落物品簡易整理表](https://docs.google.com/spreadsheets/d/1W8vbAFTSxkcCTrkHTSxJcyw92hJLgeTSZImWncjcaps/edit)
  - [頭具頁籤](https://docs.google.com/spreadsheets/d/1W8vbAFTSxkcCTrkHTSxJcyw92hJLgeTSZImWncjcaps/edit?gid=425293828)
  - [衣服頁籤](https://docs.google.com/spreadsheets/d/1W8vbAFTSxkcCTrkHTSxJcyw92hJLgeTSZImWncjcaps/edit?gid=851818185)
  - [披肩頁籤](https://docs.google.com/spreadsheets/d/1W8vbAFTSxkcCTrkHTSxJcyw92hJLgeTSZImWncjcaps/edit?gid=2115395774)
  - [鞋子頁籤](https://docs.google.com/spreadsheets/d/1W8vbAFTSxkcCTrkHTSxJcyw92hJLgeTSZImWncjcaps/edit?gid=144947816)
  - [盾頁籤](https://docs.google.com/spreadsheets/d/1W8vbAFTSxkcCTrkHTSxJcyw92hJLgeTSZImWncjcaps/edit?gid=787216853)
  - [飾品頁籤](https://docs.google.com/spreadsheets/d/1W8vbAFTSxJcyw92hJLgeTSZImWncjcaps/edit?gid=515713282)

### 怪物資料
怪物資料來自幻想廳 RO 資料庫：

- [幻想廳 RO 資料庫](https://rd.fharr.com/db/monsterlist?v=1&page=1)
- 包含 1000+ 個怪物，等級範圍 1-250 級
- 資料來源：幻想廳 RO 資料庫，經整理後儲存為 `monsters_updated.json`

## 🚀 使用方式

### 線上使用
直接訪問 GitHub Pages 網址即可使用。

### 本地開發
1. 克隆專案到本地
2. 啟動本地伺服器（解決 CORS 問題）：
   ```bash
   # 使用 Python
   python -m http.server 8000
   
   # 或使用 Node.js
   npx serve .
   ```
3. 開啟瀏覽器訪問 `http://localhost:8000`

## 📁 專案結構

```
ro/
├── index.html                    # 主頁面
├── README.md                    # 專案說明
├── .gitignore                   # Git 忽略檔案
└── src/
    └── data/
        ├── items.json           # 裝備資料
        └── monsters_updated.json # 怪物資料（更新版）
```

## 🛠️ 技術架構

- **前端**: 純 HTML + CSS + JavaScript
- **資料格式**: JSON
- **部署**: GitHub Pages
- **設計**: 響應式設計，支援多裝置

## 🔄 資料更新

### 裝備資料更新
資料會定期從 Google 試算表同步更新。如需更新資料：

1. 修改 Google 試算表內容
2. 更新 `src/data/items.json` 檔案
3. 提交並推送到 GitHub

### 怪物資料更新
怪物資料已更新為 `monsters_updated.json`：

1. 資料來源：幻想廳 RO 資料庫
2. 包含 1000+ 個怪物，等級範圍 1-250 級
3. 如需更新，請重新整理資料並替換檔案

## 📝 授權

本專案僅供學習和研究使用。所有遊戲資料版權歸原遊戲公司所有。

## 🤝 貢獻

歡迎提交 Issue 和 Pull Request 來改善這個專案！

---

**注意**: 由於瀏覽器 CORS 政策限制，本地開啟 HTML 檔案可能無法正常載入資料。請使用本地伺服器或部署到 GitHub Pages 來正常使用。 