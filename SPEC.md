# TUTTIARTS Single Page Website 規格與維護文件

## 專案概述

本專案為 TUTTIARTS 古典音樂節單頁式網站切版，依照提供的 UI/UX 設計稿製作。頁面採用 HTML5、Bootstrap 5 與自訂 CSS，整體視覺以深黑色、白色、留白與大圖為主，呈現極簡、高雅的古典音樂節風格。

目前所有 Bootstrap CSS/JS 與圖片素材皆使用本地端檔案，不依賴 CDN。

## 技術架構

- HTML：`index.html`
- CSS Framework：Bootstrap 5，本地檔案
- JavaScript：Bootstrap Bundle，本地檔案
- 自訂樣式：`css/style.css`
- 圖片素材：`images/`

## 目錄結構

```text
web 2.0/
├── index.html
├── SPEC.md
├── css/
│   ├── bootstrap.min.css
│   └── style.css
├── js/
│   └── bootstrap.bundle.min.js
└── images/
    ├── LOGO.png
    ├── img-01.jpg
    ├── img-02.jpg
    └── img-03.jpg
```

## HTML 引用規則

`index.html` 目前於 `<head>` 載入以下 CSS：

```html
<link href="css/bootstrap.min.css" rel="stylesheet">
<link href="css/style.css" rel="stylesheet">
```

頁尾載入 Bootstrap JavaScript：

```html
<script src="js/bootstrap.bundle.min.js"></script>
```

維護時請保留 Bootstrap 在前、自訂 CSS 在後的順序，確保 `style.css` 可以覆寫 Bootstrap 預設樣式。

## 頁面區塊

頁面由上至下包含以下區塊：

1. 固定式主選單 Navbar
2. Hero 主視覺區
3. 人物介紹區 Intro
4. 日程卡片區 Schedule
5. Footer 頁尾資訊
6. Back to Top 回頂部按鈕

## 圖片對應

目前圖片皆放於 `images/` 資料夾：

| 檔案 | 用途 | 引用位置 |
| --- | --- | --- |
| `LOGO.png` | 頁首與頁尾 Logo | `index.html` |
| `img-01.jpg` | Hero 首頁背景圖 | `css/style.css` |
| `img-02.jpg` | 人物介紹區圖片 | `index.html` |
| `img-03.jpg` | Schedule 四張卡片圖片 | `index.html` |

注意：因為 Hero 背景圖是在 `css/style.css` 內引用，路徑需從 `css/` 資料夾往上一層：

```css
url("../images/img-01.jpg")
```

其他 HTML 內圖片則使用：

```html
src="images/檔名"
```

## 主要樣式設定

自訂樣式集中於 `css/style.css`。

### 色彩

```css
:root {
  --night: #0B0B0B;
  --ink: #1B1E23;
  --soft-white: #F4F4F4;
  --muted: rgba(255, 255, 255, .68);
  --line: rgba(255, 255, 255, .24);
}
```

### Navbar

主選單固定於畫面頂部：

```css
.navbar {
  min-height: 74px;
  background: rgba(0, 0, 0, .3);
  border-bottom: 1px solid rgba(255, 255, 255, .08);
}
```

目前選單背景為黑色、透明度 30%，且沒有模糊效果。

### Logo

Logo 圖片寬度：

```css
.brand-logo {
  width: 112px;
  height: auto;
  display: block;
}
```

若更換 Logo，建議保持透明背景 PNG，並視覺檢查桌機與手機版尺寸。

## RWD 響應式規則

目前主要斷點：

- `max-width: 991.98px`：平板與手機選單、Hero 高度、Intro 間距調整
- `max-width: 575.98px`：手機版 Navbar 高度、Hero 高度、卡片圖片高度與 Footer 間距調整

Schedule 區塊使用 Bootstrap Grid：

```html
<div class="col-sm-6 col-lg-3">
```

效果：

- 桌機：4 欄
- 平板：2 欄
- 手機：1 欄

## 內容維護位置

### 主選單

位於 `index.html` 的 `<nav>` 區塊。若新增頁內錨點，請同步確認對應區塊是否有相同 `id`。

目前選單項目：

- Home：`#top`
- About：`#about`
- Music：`#music`
- Concert：`#schedule`
- Member：`#footer`

注意：目前頁面尚未建立獨立 `id="music"` 區塊，如需啟用 Music 導覽，建議新增對應 section 或調整連結。

### Hero 標題

位於：

```html
<h1 class="hero-title mx-auto">
```

### 人物介紹文字

位於 `section.intro` 內的：

```html
<p class="intro-copy mb-0">
```

日程列表位於：

```html
<ul class="event-list list-unstyled mb-0">
```

### Schedule 卡片

位於 `section.schedule` 內，每張卡片使用 Bootstrap Card 結構：

```html
<article class="card event-card">
```

若要新增或刪除卡片，請維持欄位 class：

```html
col-sm-6 col-lg-3
```

### Footer

位於 `footer.footer`，包含：

- Logo
- 公司簡介
- 版權宣告
- 社群連結
- 網站與 Email 聯絡資訊

目前社群圖示為純文字符號，未使用 Font Awesome 或其他外部 icon library。

## 維護注意事項

- 不要把自訂 CSS 寫回 `index.html`，請統一維護在 `css/style.css`。
- Bootstrap 檔案請保留於 `css/` 與 `js/` 資料夾。
- 若新增圖片，請放在 `images/` 資料夾。
- 若圖片由 CSS 引用，路徑需使用 `../images/檔名`。
- 若圖片由 HTML 引用，路徑需使用 `images/檔名`。
- 若更換 Bootstrap 版本，需測試 Navbar collapse、Grid 與 Card 樣式是否正常。
- 若新增外部字型、icon 或第三方套件，請優先下載至本地端再引用，以維持離線可用性。

## 建議測試項目

每次修改後建議檢查：

1. 桌機寬度下 Navbar 是否固定且 Logo 正常顯示。
2. 手機寬度下漢堡選單是否可開合。
3. Hero 背景圖是否正常載入。
4. Intro 人物圖是否正常顯示且不變形。
5. Schedule 卡片是否在桌機 4 欄、平板 2 欄、手機 1 欄。
6. Footer 社群與聯絡資訊是否排列正常。
7. Back to Top 按鈕是否可回到頁首。

## 目前版本狀態

- Bootstrap：本地端 Bootstrap 5 檔案
- 外部 CDN：無
- 自訂 CSS：已獨立為 `css/style.css`
- 圖片：全部使用本地端 `images/` 資料夾
- 頁面型態：Single Page
