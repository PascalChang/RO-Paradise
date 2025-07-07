# RO 掉落物品查詢系統

一個基於 Vue 3 的仙境傳說（RO）武器掉落查詢系統，提供快速搜尋和篩選功能。

## 功能特色

- 🔍 **智能搜尋**：支援物品名稱、職業限制、掉落魔物搜尋
- 🎯 **多重篩選**：按武器系列、等級限制篩選
- 📊 **排序功能**：點擊欄位標題進行排序
- 📱 **響應式設計**：支援手機、平板、桌面裝置
- 📄 **分頁顯示**：每頁顯示 20 個物品，提升載入速度
- 🎨 **現代化 UI**：美觀的漸層背景和卡片式設計

## 技術棧

- **Vue 3** - 前端框架
- **Vite** - 建置工具
- **CSS Grid/Flexbox** - 響應式佈局
- **JSON** - 資料儲存

## 快速開始

### 安裝依賴
```bash
npm install
```

### 開發模式
```bash
npm run dev
```

### 建置生產版本
```bash
npm run build
```

### 預覽生產版本
```bash
npm run preview
```

## 專案結構

```
ro/
├── public/
│   └── index.html          # HTML 入口檔案
├── src/
│   ├── App.vue            # 主要應用程式元件
│   ├── components/
│   │   └── ItemTable.vue  # 物品表格元件
│   ├── data/
│   │   └── items.json     # 物品資料檔案
│   └── main.js            # Vue 應用程式入口
├── package.json           # 專案配置
├── vite.config.js         # Vite 配置
└── README.md              # 專案說明
```

## 資料格式

物品資料採用 JSON 格式，每個物品包含以下欄位：

```json
{
  "名稱": "木錘 [4]",
  "職業限制": "初學者 / 劍士系列 / 服事系列 / 商人系列",
  "等級限制": "2",
  "武器等級": "1",
  "系列": "鈍器",
  "掉落魔物": "綠綿蟲"
}
```

## 部署到 GitHub Pages

1. 建置專案：
   ```bash
   npm run build
   ```

2. 在 GitHub 建立新的 repository

3. 上傳建置後的 `dist` 資料夾內容到 repository

4. 在 repository 設定中啟用 GitHub Pages，選擇 `main` branch 或 `docs` folder

## 自訂資料

要新增或修改物品資料，請編輯 `src/data/items.json` 檔案。資料格式請參考上述範例。

## 瀏覽器支援

- Chrome 60+
- Firefox 55+
- Safari 12+
- Edge 79+

## 授權

MIT License

## 貢獻

歡迎提交 Issue 和 Pull Request！

---

**資料來源**：RO 掉落物品簡易整理表 