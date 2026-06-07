# 居院 — 精品抱枕批發目錄

> 品牌官方批發目錄網站，提供批發客戶商品瀏覽與查詢服務。

🌐 **線上網址**：[https://hsh0604.github.io/HSH.github.io-GU-Pillow/](https://hsh0604.github.io/HSH.github.io-GU-Pillow/)

---

## 專案概述

| 項目 | 說明 |
|------|------|
| 品牌 | 居院 |
| 類型 | 靜態 HTML 單頁網站 + 後台管理系統 |
| 商品數量 | 70 款抱枕 |
| 部署平台 | GitHub Pages |
| 後台管理 | `admin.html`（瀏覽器端，IndexedDB 儲存）|

---

## 商品系列

| 系列 | 款數 |
|------|------|
| 簡約條紋風 | 6 款 |
| 奢華皮革風 | 13 款 |
| 拼接撞色風 | 26 款 |
| 手工工藝風 | 10 款 |
| 毛絨質感風 | 15 款 |

---

## 檔案結構

```
抱枕批發網站/
├── index.html          # 前端網站主檔（自動產生，圖片用 URL，約 67KB）
├── admin.html          # 後台管理系統
├── products_v2.json    # 商品資料備份（含圖片 base64）
├── README.md           # 本文件
├── CHANGELOG.md        # 版本更新紀錄
├── gen_index.py        # 前端 HTML 產生腳本（Python，緊急備援用）
├── deploy.py           # GitHub 批量上傳腳本（緊急備援用）
└── 居院網頁製作說明.md   # 原始製作說明

GitHub Repository 結構：
├── index.html          # 前端網站（67KB）
├── admin.html          # 後台管理
├── images/             # 商品圖片資料夾（70 張，各自獨立 JPG）
│   ├── G-14B260001.jpg
│   ├── G-14B260002.jpg
│   └── ...（共 70 張）
├── README.md
└── CHANGELOG.md
```

---

## 後台管理系統功能

### 商品管理
- 新增 / 編輯 / 刪除商品
- 商品欄位：產品型號、類別、產品圖片、品名、商品描述、尺寸(CM)、庫存
- 庫存可直接在表格內修改
- 圖片上傳自動壓縮（800px / JPEG 80%）
- **一鍵去背**（瀏覽器端 AI，完全免費）

### 資料管理
- 匯入 JSON（含圖片完整還原）
- 匯入 Excel（自動對應欄位）
- 匯出 JSON 備份
- **重複料號檢查**：有任何一筆重複即阻擋匯入

### 發布系統
- 一鍵產生前端 `index.html`（約 67KB，不含圖片）
- 圖片自動上傳至 GitHub `images/` 資料夾（智慧快取，只上傳有變動的圖片）
- 透過 Supabase Edge Function 代理安全推送至 GitHub
- 預覽 HTML（不影響線上網站）
- 部署紀錄即時顯示

### 安全性
- 登入驗證（帳號 + 密碼）
- Session 管理（關閉分頁自動登出）
- GitHub Token 存於 Supabase 伺服器端，不暴露於瀏覽器

---

## 部署方式

### 自動部署（推薦）
1. 開啟 `admin.html`，登入後台
2. 修改商品資料
3. 點選左側「🚀 發布到網站」
4. 點「🚀 產生並發布」
5. 等待 1–2 分鐘，GitHub Pages 自動更新

### 手動部署
```bash
# 執行 Python 腳本產生 index.html
python gen_index.py

# 使用 GitHub API 或直接上傳至 Repository
```

---

## 設計規範

### 字體
| 用途 | 字體 | 字重 |
|------|------|------|
| 品牌標題（英文） | Cormorant Garamond | 300/400 |
| 中文標題、品名 | Noto Serif TC | 400/500 |
| 內文、UI 元素 | Noto Sans TC | 300/400 |

### 色彩
```css
--cream:      #faf8f4   /* 頁面底色 */
--warm-white: #f5f2ec   /* Hero 背景 */
--sand:       #e8e0d4   /* 分隔線 */
--taupe:      #b5a898   /* 次要文字 */
--brown:      #7a6355   /* 描述文字 */
--dark:       #2c2420   /* 主色 */
--accent:     #9b8470   /* 強調色 */
--img-bg:     #ede8e0   /* 圖片底色 */
```

---

## GitHub 設定

| 項目 | 說明 |
|------|------|
| 帳號 | HSH0604 |
| Repository | HSH.github.io-GU-Pillow |
| Token 到期 | 2027-05-31 |
| Pages 分支 | main / root |

---

## 發布流程說明

### 正常發布（後台操作）
1. 登入後台 → 修改商品資料
2. 左側點「🚀 發布到網站」
3. 點「🚀 產生並發布」
4. 系統自動：① 上傳有變動的圖片到 `images/` ② 產生並上傳 67KB 的 HTML
5. 等待 1–2 分鐘後按 `Ctrl+Shift+R` 重新整理前台

### 緊急備援（Python 腳本）
```bash
# 重新產生 index.html（從 products_v2.json）
python gen_index.py

# 上傳所有檔案到 GitHub
python deploy.py
```

## 注意事項

- `index.html` 現為純文字 + 圖片 URL，約 **67KB**（v1.1.0 架構改版後）
- 圖片存於 GitHub `images/` 資料夾，共 70 張
- Token 到期（2027-05-31）後需至 GitHub Developer Settings 重新 Regenerate，並更新 Supabase Edge Function
- 後台商品資料存於瀏覽器 **IndexedDB**，換電腦需先「匯出 JSON」再「匯入 JSON」
- 去背功能採 Canvas Flood Fill 演算法，純瀏覽器端執行，無需費用
- Supabase Edge Function 代理：`github-proxy` v4（ap-southeast-1）

---

*居院抱枕批發目錄 — 後台管理系統 v1.1.0*
