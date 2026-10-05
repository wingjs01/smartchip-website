# 英文修正版部署說明

## 交付內容

`deliverables/en_fixed/` 共 118 個 HTML 檔，直接覆蓋網站根目錄的同名檔即可。版型、CSS、圖片、JS 和相對路徑都沒動，只改文字和 `<head>`。

不包含的檔案（請保留原檔，改用 `.htaccess` 的 301 處理，見 `deliverables/htaccess_additions.txt`）：
- `index.html`（根目錄 JS 轉址頁，裡面有 Shopee / ihoin.com 的判斷邏輯，我沒動）
- `ridm1/3/4`、`raboutApp1/2`、`ricdesign2`、`ranimal1`、`rrfid-elock1`、`rhlf_nfc-rfid` 這 9 個舊轉址頁

## 改了什麼

### 內容（`<body>`）
1. **中文段落全部翻成英文**：IC 系列 6 頁、active_at01、active_r01、news、smartKeyK1、「前往購買」「如何使用」、頁尾中文地址、圖片 alt 的中文檔名。
2. **機器翻譯亂碼段落重寫**：522F/FS/S/AUS-2、5238、53105、LF 模組 6 頁、長距離讀頭 4 頁、idm、software、animal、pet、undermark、personnelLocation、bike 系列、rfid-elock、smartCarCharge、aboutApp、solution_beacon 等。
3. **拼字錯誤**：約 40 處（Demensions、Prompy、Weigth、Colro、hsa、sever you…）。
4. **規格／型號**：
   - K1 頁 13.56 KHz → MHz
   - 5237 頁 20mAh → 20 mA
   - 電池容量 mA → mAh
   - SMC632AS 頁內文型號 SMC632ES → SMC632AS/AUS
   - SMC5227 頁內文型號 SMC-P135125S → SMC5227
   - 5220S-R 的標題不再寫 ISO14443A（改為 125 kHz）
   - G13421 生物晶片刪掉誤植的「laundry code」
5. **全站統一**：全形標點改半形；kHz / MHz / GHz 寫法；MIFARE、DESFire、Ultralight、RoHS、IoT、Wiegand；"an Unique" → "a unique"；"Build-in" → "Built-in"。
6. **頁尾**：Copyright 2015–2017 → © 2026 SMARTCHIP (SMC)。
7. **About 頁**：原本只有圖片，在圖片下方加了英文文字版（沿革、事業領域、據點），讓 AI 讀得到。
8. **knowledge.html**：疑似轉載的「Long Answer」那幾段已依同樣的技術事實重新撰寫，不再是原文。
9. **死連結**：personnelLocation 指向 4 個 404 頁的連結，改指向現有的 active_* 頁。

### `<head>`
- `<html lang="en">`（原本 22 頁誤標 zh-Hant-TW、1 頁 "cn"、1 頁有控制字元）
- 每頁獨立的英文 title，118 頁沒有重複。格式：`型號 + 產品類型 | SMC Smartchip`
- 每頁獨立的英文 meta description（取代原本的中文描述）
- Open Graph、canonical
- hreflang：en / zh-Hant / zh-Hans / ja / x-default
- JSON-LD：首頁是 Organization，產品頁是 Product，其他頁是 BreadcrumbList
- 404 頁加上 `noindex`

## 部署順序（重要）

1. 備份根目錄所有 `.html`。
2. 上傳 `en_fixed/*.html` 覆蓋根目錄。
3. **英文頁的 hreflang 指向 `/jp/`**，所以請和日文版同一批上線。如果日文版要晚點上，先刪掉每頁的 `hreflang="ja"` 那一行，否則會指向 404。
4. 一起上傳 `robots.txt`、`sitemap.xml`、`llms.txt`、`.htaccess` 規則和 `js_patch/`（說明見 `JP_部署說明.md`）。
5. 到 Google Search Console 重新提交 sitemap，並抽查幾頁做「網址檢查」。

## 我沒改、需要你們確認的地方

這些需要原始資料，我不能用猜的：

| 頁面 | 問題 |
|---|---|
| `HF_R_5220f.html` | 產品編號是 SMC522F，但內文描述的是「SMC5220S series」，請確認這頁到底是哪個產品 |
| `HF_R_btUltralight.html` | 頁名是 Ultralight（13.56 MHz），規格表卻是 125/134.2 kHz、FDX-B，疑似從低頻頁複製 |
| `FM8128E020.html` | Output power「10~3 dBm」，疑為 10~30 dBm |
| `about.html` | 數字動畫「90% Market Share for RFID Chips in China」（寫在 `about.min.js`），請確認有依據 |
| `IC_5326s-3.html` 等 | 特點清單第 9 點排在第 8 點前面，原始資料就是這樣 |
| 全站 | 公司正式英文名稱。目前 title 用「SMC Smartchip」，JSON-LD 用法定名「瑞新電子股份有限公司」加別名 SMC / SMARTCHIP。決定正式英文名後，改 `build_en.py` 裡的 `SUFFIX` 和 `jsonld()` 再重新產生即可 |
| 全站 | Google Analytics 仍是已停用的 UA 代碼，需要你們建 GA4 後換掉 |

## 重新產生

```bash
cd smartchip
python build_en.py
```

修正對照表在 `tr/en_fix_*.txt`（格式：`段落編號<TAB>修正後英文`），自動規則（標點、單位、品牌大小寫）在 `build_en.py` 的 `AUTO`。

## 本機預覽

```bash
python smartchip/preview_server.py
```

修正版：http://localhost:8765/en/indexsmartchip.html
日文版：http://localhost:8765/jp/indexsmartchip.html
