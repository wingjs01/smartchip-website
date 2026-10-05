# smartchip.com.tw 英文站稽核報告

- 掃描日期：2026-10-03
- 範圍：`https://www.smartchip.com.tw/` 根目錄英文站，共 132 個網址（128 頁 200 OK、4 頁 404），另含 sitemap、robots、JS 和 About 頁的圖片
- 方法：從首頁和 sitemap 遞迴爬取 → 抽出可見文字（1,580 段不重複文字，約 9 萬字元）→ 人工逐段校對；SEO/AI 可讀性用腳本統計
- 原始資料：`pages/`（HTML）、`text/`（每頁純文字）、`unique_lines.txt`（全站不重複句子，含出處頁）

---

## 總結（先看這段）

| 嚴重度 | 問題 | 影響 |
|---|---|---|
| 🔴 高 | **英文站有 10 頁整頁或大段是中文**（IC 系列 6 頁、active_at01、active_r01、news、smartKeyK1） | 外國客戶看不懂；AI 判定語言錯亂 |
| 🔴 高 | **約 15 頁是早期機器翻譯的亂碼英文**（"mold train"、"communication agreement"、"locomotive lock"…） | 嚴重傷害專業形象，AI 摘要也會照抄錯誤 |
| 🔴 高 | **115 頁英文頁的 meta description 是中文**，全站只有 4 種描述 | Google/AI 摘要顯示中文或重複文字 |
| 🔴 高 | **首頁「/」只有 JS 轉址、沒有內容**；http→https 也只靠 JS | 大部分 AI 爬蟲（GPTBot、ClaudeBot、PerplexityBot）不執行 JS，看到的是空頁 |
| 🔴 高 | **Google Analytics 還在用 UA-84670428-1（Universal Analytics）** | UA 已在 2023–2024 停用，**網站目前沒有任何流量數據** |
| 🟠 中 | 單位錯誤：電池容量寫 mA（應為 mAh）、工作電流寫 mAh（應為 mA）、K1 寫 13.56 **KHz**（應為 MHz） | 規格錯誤，工程師客戶會直接質疑 |
| 🟠 中 | 型號複製貼上錯誤（SMC632AS 頁寫 SMC632ES、SMC5227 頁寫 SMC-P135125S、低頻模組標成 ISO14443A…） | 規格可信度 |
| 🟠 中 | 標題重複/錯誤：128 頁只有 82 種 title；13 個 UHF 標籤頁 title 是「Biochip Series」；5 個 SMC632 頁 title 是「SMC65327M-3CP」 | 搜尋結果和 AI 引用張冠李戴 |
| 🟠 中 | 4 個 404 頁仍在 sitemap 或被連結（`2.4G_r01`、`2.4G_24gTag` 由 personnelLocation 連出） | 死連結 |
| 🟡 低 | 錯字約 40 處、全形標點混在英文裡（`：，。、（）`）、kHz/MHz 大小寫不一 | 細節品質 |
| 🟡 低 | 內容過期：Copyright 2015–2017、最新新聞 2017/11、「20 years」（1995 年起算已 31 年） | AI 會優先引用新內容 |

---

## 一、英文錯誤清單

### 1-1 英文站上的中文內容（要整段翻成英文）

| 頁面 | 中文內容 |
|---|---|
| `IC_51541.html` | 整頁規格、特點、腳位說明都是中文 |
| `IC_5326p-3.html` | 整頁中文 |
| `IC_5326s-3.html` | 整頁中文 |
| `IC_65327m-3cp.html` | 整頁中文 |
| `IC_995326-44dbs.html` | 整頁中文 |
| `IC_qw18s.html` | 整頁中文（而且 `<html lang="cn">` 是無效的語言碼） |
| `active_at01.html` | 「產品編號：」、產品描述整段、「1、1.5、2、3 秒」 |
| `active_r01.html` | 「產品編號：」、產品描述整段 |
| `news.html` | SMC5220s、SMC522s 兩則新聞內文、「前往了解」 |
| `smartKeyK1.html` | 標題「A1 可攜式NFC讀寫器」（內文是 **K1**，型號也錯）、整段介紹和產品特色 |
| `HF_Tag_MIFARE-Classic-1k.html` | 按鈕「前往購買」→ **Buy Now** |
| `aboutApp.html` | 「iHoin智慧車充」、「兩種等級的保護，可以放心備份或上傳！」、「搭配硬體晶片，難以破解」 |
| `smartCarCharge.html` | 「如何使用」→ **How to Use** |
| `ugftag01/11.html` 等 4 頁 | 「直徑 31mm / Diameter 31mm」→ 刪掉中文 |
| `HF_Module_5237` 等 4 頁 | 頁尾地址「23557 新北市中和區橋和路11號16樓」→ 改用英文地址 |
| `active_rfid_solution_reader_handle.html` | 「Back camera 1300万 / Front camera 500万」→ **Rear camera 13 MP / Front camera 5 MP** |
| `SMC52300_41/42/50`、`SMC55232`、`beacon` 等 | title 中英混用「- 瑞新電子」、「- Ruixin Electronics」、「- SMC」三種寫法 |

### 1-2 機器翻譯亂碼（建議整段重寫）

這些段落是逐字直譯的中文，母語人士讀不懂，修錯字救不回來。

**`HF_R_522f.html`、`HF_R_522fs.html`、`HF_R_522s.html`、`HF_R_522u.html`（同一段複製 4 次）**
> ❌ "SMC522F is 13.56Mhz the Mifare non-contact induction type reader **a mold train**, the mold train uses the SMC original factory chip … **communication agreement** … **the user any MCU motherboard connected connection letter**."

✅ 建議改寫：
> The SMC522F is a 13.56 MHz contactless MIFARE reader module built on SMC's in-house SMC522 chip. It is easy to integrate and cost-effective, making it ideal for device development, card-reader development and RFID terminal design. The module reads SMC4111 UIDs and reads/writes ISO14443A cards, including the MIFARE series. It runs at 3.3 V and connects directly to any MCU board through a simple UART interface.

這 4 頁表格裡的欄位名也要改：

| ❌ 原文 | ✅ 修正 |
|---|---|
| Note: This product accepts the guest to make the service, … the communication agreement … | Note: Customization is available. Operating frequency, interface, communication protocol and operating mode can be tailored to customer requirements. |
| Correspondence interface | Communication interface |
| reader the card distance / reader the card time | Read range / Read time |
| Corresponds the transmission speed in series | Serial baud rate |
| Watch-dog protection / In sets at the hardware watch-dog | Watchdog / Built-in hardware watchdog |
| UART（May expand isRS-232或RS-485） | UART (expandable to RS-232 or RS-485) |
| Has 1 assistance output, may control LED or the buzzer and so on the external instrumentation | 1 auxiliary output for driving external devices such as an LED or buzzer |
| SMC522S simplification instruction reader module | SMC522S Simplified-Command Reader Module |
| supports Mifare S50/S70 **the material read-write** operation … only must use the simple 3 orders (reading according to, write material and revision key) | supports MIFARE S50/S70 read/write. Only three simple commands are needed (Read Data, Write Data, Change Key). |

**`idm.html` "Why should you choose SMC?"**
> ❌ "SMC has various types product design experience to be special, in which is most prominent by the non-contact induction type product … from the components, **the mold train**, the end product to **the soft hardware system conformity**, is a vertical conformity group company."

✅ 建議改寫：
> SMC has extensive design experience across many product types, especially contactless (RFID/NFC) products. Our team covers digital, analog, wired, wireless and power-management ICs, and we have in-house manufacturing. From components, modules and finished products to hardware–software system integration, SMC is a vertically integrated company.

同頁還有：

| ❌ | ✅ |
|---|---|
| SMC has been **plowing** Taiwan market for 20 years | SMC has served the Taiwan market for over 30 years |
| we have **product lines** … with iso 9001 | we have **production lines** … with ISO 9001 certification |
| all **one-handed** arrangements | all handled by one team |
| SMC started at chip design, **priding** from modules … | Starting from chip design, SMC covers everything from modules to finished products |
| eliminating the time you consult around | saving you the time of dealing with multiple vendors |

**`software.html`**

| ❌ | ✅ |
|---|---|
| We are anxious to be able to **sever** you. | We look forward to **serving** you. |
| Leave your idea up to me! | Leave your ideas to us! |
| Do you have a program waiting to be developed? | Have a project that needs development? |
| … and even a variety of software to the ICON interface art design readily available | … through to UI and icon design |
| title「sofrware - SMC」 | Software - SMC |

**`LF_Module_51483/51486/51487/51488/51492/52101`**
> ❌ "SMC51486 is **induce module which frequency is 125Khz**, professional design to read SMC4001, Output from **WEIGEN** 34 …"

✅ 句型：
> The SMC51486 is a 125 kHz RFID reader module designed to read SMC4001 tags, with Wiegand 34 or ABA Track 2 output.

| ❌ | ✅ |
|---|---|
| WEIGEN / Weigan26 / Wigan 34 / Weigand | **Wiegand** 26 / Wiegand 34（全站統一） |
| lenght / (High) / (height) | length / height（51483、51487、51492） |
| m/m | mm |
| SMC self own LF closed solution, not compatible to other LF protocol | SMC's proprietary LF format, not compatible with other LF protocols, for higher security |
| … Output through.（51488 句子沒寫完） | 補完句子 |
| DATA0&DATA（52101） | DATA0 & DATA1 |

**`animal.html`**
> ❌ "…can be effective. To do food management." / "There is no regional isolation of the epidemic can also occur at any time…"

✅ 建議改寫第一段：
> RFID livestock management lets farmers monitor the growth and health of cattle, sheep and pigs. Early detection and treatment help prevent outbreaks and support food-safety management.

| ❌ | ✅ |
|---|---|
| Patented small ear design, to prevent animals bite | Patented compact design that resists biting |
| Read distance, waterproof, … anti-acid and so on. | Long read range; waterproof; resistant to high/low temperatures and acids |
| Feces, urine, temperature changes are not affected. | Unaffected by feces, urine or temperature changes |

**`undermark.html`**：整頁直譯，建議重寫。例：
> ❌ "When the underground pipe failure can be found as soon as possible when the fault point, to avoid the pipeline in order to find the excavation of the road…"
> ✅ "When a pipe fails, the fault can be located quickly without excavating the road, minimizing disruption to residents."

**`bike_*.html`、`rfid-elock.html`、`products.html`：機車被翻成火車頭**

| ❌ | ✅ |
|---|---|
| Chip **locomotive** lock（products.html） | Chip Scooter Lock |
| a smart App Bluetooth **locomotive** lock（bike_mt67b） | a smart Bluetooth scooter lock |
| Anti-theft and **wisdom**（首頁輪播，智慧→wisdom） | Smart anti-theft |
| Music searching **car** module | Sound-based Scooter Locator |
| many cars have USB charging as **stander** equipment … implemented to **car modes** | … as **standard** equipment … implemented in **scooter models** |
| SMC-m93u（內文）vs SMC-mt93u（標題） | 統一型號 |
| Smart **Eletronic** Motorcycle Key | Smart **Electronic** Motorcycle Key |
| If a thief use a non-signal matching key … it can not be launched | If a thief uses a key without the matching chip, the engine cannot be started |
| as the car generally has a deterrent effect | acting as a deterrent |

**`personnelLocation.html`、`pet.html`**

| ❌ | ✅ |
|---|---|
| Personal Control | Personnel Monitoring |
| the movement of staff … or the **absent** of staff | … or the **absence** of staff |
| prevent livestock from getting **loss** | from getting **lost** |
| When pets or children **lose** | When pets or children **go missing** |
| Top locations statistics | Hot-spot analytics |
| Twice one second / Can be used for four months | Transmits twice per second; battery life approx. 4 months |
| hand-code reader（pet） | handheld reader |
| Global unique serial number to ensure the uniqueness of animal **wafer** serial numbers | Globally unique serial number for each animal **chip** |
| Effectively prevent static breakdown, pressure more than 5000v | ESD protection > 5 kV |
| In line with the national standard disposable syringes | Supplied in standard disposable syringes |

**`knowledge.html`**

| ❌ | ✅ |
|---|---|
| What is the difference between NFC and RFID, or even different? | What is the difference between NFC and RFID? |
| In accordance with the different application context with the appropriate system, you can get the maximum efficiency and economic costs. | Choosing the right system for each application maximizes efficiency and minimizes cost. |
| title「Scientific and technological knowledge」 | RFID & NFC Knowledge Base |

⚠️ 「Long Answer」那幾段的文風和全站明顯不同，看起來像從國外 RFID 部落格複製的。請確認來源：如果是轉載，要重寫或註明出處，否則有著作權風險，搜尋引擎和 AI 也會判定為重複內容而降權。

### 1-3 拼字錯誤（逐字修正即可）

| 頁面 | ❌ | ✅ |
|---|---|---|
| HF_Module_5237 | Single-**andtenna** | Single-antenna |
| HF_Module_5238 | combinedISO14443A/B | combines ISO14443A/B |
| HF_R_5220f / 5220s / 5220s_n / 5220s_r | **Demensions** | Dimensions |
| HF_R_5220f / 5220s_n | integrating RF, **MUC**, and memory | RF, **MCU** and memory |
| HF_Tag_MIFARE-Classic-1k | **Dimention** / 13.56MHZ / NXP Mode | Dimensions / 13.56 MHz / NXP |
| HF_R_btMifare 等 5 頁 | **Curent** state | Current state |
| LF_R_bt134 | Product Number-BT134 | Product Number: SMC-BT134 |
| LF_R_h125 等 3 頁 | Status **Prompy** | Status Prompt |
| LF_R_h125 等 6 頁 | 9V alkaline **batteriesor** or | 9V alkaline battery or |
| LF_R_h134u | **Weigth** | Weight |
| LF_R_h125 / h126b | the foot ring | leg ring |
| LF_R_hj1000 | **mutiple** languages | multiple languages |
| LF_R_r134 | **RRS232** / DATAO, DATAI | RS232 / DATA0, DATA1 |
| LF_Tag_cl125 | Card-type **Romeot** / **ISSO**11785 | Long-range Card / ISO11785 |
| LF_Tag_g13421 | Product **Nuber** / **Colro** | Product Number / Color |
| LF_Tag_4001 | **opearting** / tags **care** made | operating / tags **are** made |
| LF_Tag_* 多頁 | **an** Unique identification code | **a** unique identification code |
| LF_Tag_* 多頁 | ROHS | RoHS |
| LF_Tag_er13424 | It can be acid (20% aqueous ammonia…) | Acid-resistant (withstands ≥12 h in 20% ammonia solution) |
| LF_Tag_g13421 | … which can act as the **laundry code** | 生物晶片不是洗衣標籤，是從 LL1252203 複製來的，要刪 |
| HF_Module_53105 | **SMC530105** | SMC53105 |
| HF_Module_53105 / HF_R_5220f | **Build-in** | Built-in |
| SMC632ES | RC**22** / PB3and GND | RC522 / PB3 and GND |
| SMC6320US | single card reading **more** | single card reading **mode** |
| icdesign | SMC RFID CHIP **hsa** | has |
| about（圖片 alt） | design **integratyon** manufacturing | integration |
| aboutApp | battery **voltag** / **thebattery** / supporting **out** latest version / how can you read | voltage / the battery / our / how you can read |
| smartkeyA1 | Li-**batery** | Li-battery |
| solution_smc5094 | Wine & Spirit:： | Wine & Spirits: |
| solution_beacon / solution | regular.intervals / it will . / used as . | 多餘的句點與斷行要清掉 |
| active_rfid_solution_reader | 50meters above | over 50 m |
| active_rfid_solution_tag | up to 0–30m | up to 30 m |
| active_at01 | Up to 100 **volume labels** per second / Encryption **Calculus** / < 6.0 **ua** | 100 tags per second / encryption algorithm / < 6.0 µA |
| ugftag01–13 | Re / Write / Depend on reader / lane system | Read/Write / Depends on reader / lane (toll/parking) systems |
| animal、solution | Pets Management solution | Pet Management Solution |
| 404 | title「under construction」 | Page Not Found - SMC |

### 1-4 規格／型號錯誤（請工程確認，影響最大）

| 頁面 | 問題 |
|---|---|
| `smartKeyK1.html` | Frequency 寫 **13.56 KHz**，應為 **13.56 MHz** |
| `HF_Module_5237` | Dynamic Operating Current **20mAh**：電流單位應為 **mA** |
| `HF_R_P135`、`SMC6320US`、`HLF_R_*` | built-in rechargeable **500mA** battery：容量單位應為 **mAh** |
| `HF_R_btMifare` 等 | 3.7V **1700mA** Li-Battery、3200mA：應為 **mAh** |
| `SMC632_AS_US.html` | 內文寫「The **SMC632ES** series…」，應為 SMC632AS/AUS |
| `smc5227v4.html` | 內文寫「The **SMC-P135125S** is…」，應為 SMC5227 |
| `HF_R_5220f.html` | Product Number SMC522F，但內文寫「SMC5220S series」 |
| `LF_R_5220s_r.html` | 125 kHz 低頻模組，H1 和 title 卻寫「**ISO14443A** Reader module」（14443A 是高頻） |
| `HF_R_btUltralight.html` | 頁名是 Ultralight（13.56 MHz），規格表卻是 125/134.2 kHz、SMC4001、FDX-B，看起來是從低頻頁複製的 |
| `FM8128E020.html` | Output power「10~3 dBm」：疑為 10~30 dBm |
| `about.html` | 數字動畫寫「90% Market Share For RFID Chip in China」：這個宣稱要有依據，否則建議改寫或拿掉 |

### 1-5 全站一致性

- **全形標點**：英文句子裡大量使用 `：`、`，`、`。`、`、`、`（）`，例如「Product Number：」出現在幾乎每一頁。全部換成半形 `: , . ( )`。
- **單位寫法**：kHz（不是 KHz/Khz/KHZ）、MHz（不是 Mhz/MHZ）、GHz、mAh、µA；數字和單位之間空一格（13.56 MHz）。
- **IoT**（不是 IOT）、**MIFARE**（官方大寫）、**RoHS**、**Wiegand**。
- **公司英文名不統一**：SMC / SMARTCHIP / SMARTCHIP MICROELECTRONIC / Ruixin Electronics / 瑞新電子。請決定一個正式英文名，例如「Smartchip Microelectronic Corp. (SMC)」，全站和 meta 統一。這件事對 AI 辨識「這是同一家公司」很關鍵。

---

## 二、讓 AI 容易爬到、引用你們的建議

### 現況診斷（實測）

| 檢查項 | 結果 |
|---|---|
| `robots.txt` | ❌ 404，不存在 |
| `llms.txt` | ❌ 404，不存在 |
| `sitemap.xml` | ⚠️ 2018 年產生、全是 http://、列了 4 個 404 頁、缺新產品頁（5240H、5241、FR24、HR24、S-TAG） |
| 首頁 `/` | ❌ 704 bytes，只有 `<script>` 轉址，沒有內容 |
| http→https | ❌ 只靠 `checkurl.js`，伺服器回 200 而不是 301 |
| `r*.html`（ridm1、raboutApp1 等 10 頁） | ❌ JS 轉址頁，而且 title 都是「SMC51483 RFID Module」 |
| hreflang / canonical | ❌ 0 頁 |
| 語言切換 | ❌ 用 JS 動態產生，爬蟲看不到 /tw/、/cn/ 版本的對應關係 |
| `<html lang>` | ⚠️ 22 頁英文頁宣告成 zh-Hant-TW、1 頁是無效的「cn」、1 頁含控制字元「\x08en」 |
| 結構化資料（JSON-LD） | ❌ 0 頁 |
| Open Graph | ❌ 0 頁有 og:title |
| 圖片 alt | ❌ 669 張圖沒有 alt |
| H1 | ⚠️ 22 頁沒有 H1；首頁 H1 是一整段長文 |
| About 頁 | ❌ 公司沿革、據點、業務範圍**全部是圖片**，AI 讀不到文字 |
| 圖片檔名 | ⚠️ 21 個檔名含中文或空格（如 `操作說明_125_1.png`） |
| 分析工具 | ❌ GA Universal Analytics 已停用，沒有數據 |

### 建議改法（依效益排序）

#### P0：一天內可完成，效益最大

1. **新增 `robots.txt`**，明確允許 AI 爬蟲並指向 sitemap：
   ```
   User-agent: *
   Allow: /

   User-agent: GPTBot
   Allow: /
   User-agent: OAI-SearchBot
   Allow: /
   User-agent: ClaudeBot
   Allow: /
   User-agent: Claude-SearchBot
   Allow: /
   User-agent: PerplexityBot
   Allow: /
   User-agent: Google-Extended
   Allow: /

   Sitemap: https://www.smartchip.com.tw/sitemap.xml
   ```

2. **把 JS 轉址改成伺服器 301**。主機是 Apache（Plesk），在根目錄 `.htaccess` 加：
   ```apache
   RewriteEngine On
   # http → https，並統一成 www
   RewriteCond %{HTTPS} off [OR]
   RewriteCond %{HTTP_HOST} !^www\. [NC]
   RewriteRule ^(.*)$ https://www.smartchip.com.tw/$1 [R=301,L]
   # 首頁
   RewriteRule ^$ /indexsmartchip.html [R=301,L]
   RewriteRule ^index\.html$ /indexsmartchip.html [R=301,L]
   # r*.html 轉址頁
   RewriteRule ^ridm[134]\.html$ /idm.html [R=301,L]
   RewriteRule ^raboutApp[12]\.html$ /aboutApp.html [R=301,L]
   RewriteRule ^ricdesign2\.html$ /icdesign.html [R=301,L]
   RewriteRule ^ranimal1\.html$ /animal.html [R=301,L]
   RewriteRule ^rrfid-elock1\.html$ /rfid-elock.html [R=301,L]
   RewriteRule ^rhlf_nfc-rfid\.html$ /hlf_nfc-rfid.html [R=301,L]
   ```
   注意：`/Shopee` 和 ihoin.com 的特殊轉址邏輯要先確認，再一起寫進規則。

3. **新增 `/llms.txt`**（給 LLM 看的網站摘要，Markdown 格式）。已產出：`deliverables/llms.txt`。新興慣例，成本極低。

4. **重產 `sitemap.xml`**：全部改 https、刪掉 404 和轉址頁、加入新頁和 /tw/、/cn/、/jp/，並用 `xhtml:link hreflang` 標出語言對應。已產出：`deliverables/sitemap.xml`（117 頁 × 4 語言 = 468 個網址）。`robots.txt` 也已產出：`deliverables/robots.txt`。

5. **GA 換成 GA4**，否則看不到 AI 和搜尋帶來的流量。

#### P1：每頁的 head 修正（可以用範本批次處理）

6. **每頁獨立的 title**，格式：`{型號} {產品類型} | SMC Smartchip`，例如 `SMC5237 13.56 MHz ISO14443A/ISO15693 Reader Module | SMC Smartchip`。
7. **每頁獨立的英文 meta description**（120–160 字元，寫清楚型號、頻率、協定、介面、用途）。
8. **hreflang + canonical**（每頁的 `<head>`）：
   ```html
   <link rel="canonical" href="https://www.smartchip.com.tw/HF_Module_5237.html">
   <link rel="alternate" hreflang="en" href="https://www.smartchip.com.tw/HF_Module_5237.html">
   <link rel="alternate" hreflang="zh-Hant" href="https://www.smartchip.com.tw/tw/HF_Module_5237.html">
   <link rel="alternate" hreflang="zh-Hans" href="https://www.smartchip.com.tw/cn/HF_Module_5237.html">
   <link rel="alternate" hreflang="ja" href="https://www.smartchip.com.tw/jp/HF_Module_5237.html">
   <link rel="alternate" hreflang="x-default" href="https://www.smartchip.com.tw/HF_Module_5237.html">
   ```
9. **`<html lang>` 修正**：英文頁一律 `en`、繁中 `zh-Hant-TW`、簡中 `zh-Hans`、日文 `ja`。
10. **JSON-LD 結構化資料**：
    - 首頁放 `Organization`（正式英文名、alternateName「瑞新電子股份有限公司」、地址、電話、email、logo、FB/YouTube 的 sameAs）。
    - 每個產品頁放 `Product`（name、sku=型號、brand、description，主要規格放 `additionalProperty`）。
    - knowledge 頁放 `FAQPage`。
    - 範例見 `deliverables/jsonld_examples.html`；日文版各頁也已內建。

#### P2：內容層面（AI 引用的關鍵）

11. **About 頁改成文字**：沿革（1995 IC design house → 2002 RFID chip → 2010 total solution）、據點（台北總部/研發、深圳業務與工廠、香港業務、印度合資）、業務範圍（RFID/NFC、Memory、IoT、App、ASIC、IPC、EV、E-Lock）全部寫成 HTML 文字。圖可以保留當裝飾。
12. **補 alt**：產品圖的 alt 寫「型號 + 產品類型」，例如 `alt="SMC5237 13.56 MHz RFID reader module"`。
13. **新增「選型指南」頁**：用 HTML 表格比較 125 kHz / 134.2 kHz / 13.56 MHz / UHF / 2.4 GHz active 的讀距、協定、用途和對應型號。AI 回答「我要做門禁該用哪種 RFID 模組」這類問題時，最愛引用這種表格。
14. **擴充 FAQ**：例如「ISO14443A 和 ISO15693 差在哪」、「Wiegand 26 和 34 差在哪」、「SMC4001 和 EM4100 相容嗎」、「MOQ/客製化流程」。一題一段，問題放 H2/H3。
15. **更新時效**：Copyright 改成當年、補 2018 年後的新聞（例如 5241 支援 Apple VAS / Google Smart Tap、FR24/HR24 上市）、把「20 years」改成「since 1995」。
16. **恢復 Contact 頁**（目前選單裡被註解掉），加上英文聯絡資訊和詢價說明。
17. **圖片檔名改成英文、不用空格**，例如 `smc-c135125s-manual-1.png`。
18. **建立站外一致的實體資訊**：LinkedIn 公司頁、Google 商家檔案、經銷商/電商頁面使用同一個英文公司名和網址。AI 很依賴第三方來源來確認公司身分。

---

## 三、日文版

- 檔案：`deliverables/jp/`（128 個檔案），上傳到網站 `/jp/` 即可，既有頁面零改動
- 部署步驟、已更正的錯誤、上線前要人工確認的事項：見 `JP_部署說明.md`
- 日文版已內建第二節建議的所有 head 層級修正（lang、獨立 title/description、canonical、hreflang、JSON-LD、OG），可以直接當英文站改版的範本
