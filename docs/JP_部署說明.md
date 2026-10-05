# 日文版（/jp/）部署說明

## 交付內容

```
deliverables/
├── jp/                      ← 整個資料夾上傳到網站根目錄，成為 /jp/
│   ├── *.html               ← 128 個檔案（117 頁內容 + 首頁入口 + 404 + 9 個舊轉址頁）
│   └── js/main/main.min.js  ← 日文版語言選單（English / 繁體中文 / 简体中文 / 日本語）
├── js_patch/                ← 讓現有三個語言版的選單出現「日本語」
│   ├── root/main.min.js     → 覆蓋 /js/main/main.min.js
│   ├── tw/main.min.js       → 覆蓋 /tw/js/main/main.min.js
│   └── cn/main.min.js       → 覆蓋 /cn/js/main/main.min.js
├── robots.txt               → 放根目錄（目前不存在）
├── sitemap.xml              → 覆蓋根目錄的舊 sitemap（117 頁 × 4 語言 = 468 個網址，含 hreflang）
├── llms.txt                 → 放根目錄（給 AI 讀的網站摘要）
├── htaccess_additions.txt   → 加進根目錄 .htaccess（301 轉址）
└── jsonld_examples.html     → 英文站結構化資料範例
```

## 上傳步驟

1. **先備份**：網站根目錄的 `.htaccess`、`sitemap.xml`、`js/main/main.min.js`、`tw/js/main/main.min.js`、`cn/js/main/main.min.js`。
2. 上傳 `deliverables/jp/` → 網站 `/jp/`。
3. 上傳 `robots.txt`、`llms.txt`、`sitemap.xml` 到根目錄。
4. 用 `js_patch/` 的三個檔案覆蓋對應的 `main.min.js`。
5. 把 `htaccess_additions.txt` 的規則加進 `.htaccess`。
6. 驗證：
   - `https://www.smartchip.com.tw/jp/` → 應 301 到 `/jp/indexsmartchip.html`
   - 任一頁右上角地球選單 → 應出現「日本語」，可以在四種語言間切換到同一頁
   - `http://smartchip.com.tw/about.html` → 應 301 到 `https://www.smartchip.com.tw/about.html`
7. 到 Google Search Console 重新提交 `sitemap.xml`。

## 日文版的設計

- **零改動既有頁面**：CSS、圖片、共用 JS 都直接引用根目錄（`/css/…`、`/img/…`），不複製。/jp/ 只多一份語言選單 JS。
- **內容和英文版相同**，但英文版的錯誤在日文版已更正：
  - 機器翻譯亂碼段落：依原意重寫成通順日文
  - 英文頁裡的中文段落（IC 系列、active_at01/r01、news、K1 等）：直接翻成日文
  - 規格單位錯誤：K1 的 13.56 KHz → MHz、5237 的 20mAh → 20 mA、電池容量 mA → mAh、kHz 大小寫
  - 型號複製錯誤：SMC632AS 頁和 SMC5227 頁的內文型號已更正；5220S-R 不再標成 ISO14443A
  - 4 個失效的 2.4G 連結改指向現有的 active_* 頁
- **SEO/AI 設定（日文版已全部內建，可當英文站的改版範本）**：
  - `<html lang="ja">`
  - 每頁獨立的 title（117 頁無重複）和日文 meta description
  - canonical + hreflang（en / zh-Hant / zh-Hans / ja / x-default）
  - JSON-LD：首頁放 Organization，產品頁放 Product，所有頁都有 BreadcrumbList
  - Open Graph
  - About 頁在原本的圖片下方加了一段日文文字（沿革、事業領域、據點），讓 AI 讀得到
  - 電話改成國際格式 +886-2-8221-8800
- **knowledge.html 的「詳しい解説」**：英文原文疑似轉載外部文章，日文版沒有逐句翻譯，而是依同樣的技術事實重新撰寫。

## 上線前請人工確認

1. **日文校稿**：建議請日文母語者（或日本代理商）看過首頁、會社概要、製品一覧，以及 3–5 個主力產品頁。專有名詞譯法：カットコード（割碼）、耳標、バイオチップ。
2. **圖片內的英文**：首頁輪播第二張 `/img/高低頻-reader_en.jpg`、About 頁的 `about_en_*.png`、icdesign 的 `commentary.png` 都是內嵌英文的圖片。日文版目前沿用英文圖；要完整在地化，需要美編出日文版圖片。
3. **「中國 RFID 晶片市占 90%」**：About 頁的數字動畫寫在共用的 `about.min.js`，日文版也照樣顯示。建議確認這個宣稱有依據。
4. **Google Analytics**：所有語言版都還在用已停用的 UA 代碼，建議一起換成 GA4。
5. **公司英文正式名稱**：日文版 JSON-LD 的 alternateName 暫用 SMC / SMARTCHIP / Smartchip Microelectronic。確定正式名稱後，改 `build_jp.py` 再重新產生即可。

## 之後要更新日文版

英文站改版後重跑：

```bash
cd smartchip
python crawl.py
python segments.py
python build_jp.py
```

`build_jp.py` 會列出新增、還沒翻譯的句子（MISSING translations）。在 `tr/ja_*.txt` 補上翻譯後再跑一次即可。

## 本機預覽

```bash
python smartchip/preview_server.py
```

開 http://localhost:8765/jp/indexsmartchip.html。/jp/ 讀本機檔案，其他資源（CSS、圖片）直接代理正式站。
