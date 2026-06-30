# Design System — 彭敬鈞 (Albert Peng) 產品經理作品集

> 用途：本文件是「重構 portfolio bot / 重建這個作品集網站」的單一真實來源（single source of truth）。
> 它把目前線上 Framer 專案完整拆解成：設計 token、全站元件、逐頁規格、CMS 資料模型、長文排版系統、程式覆寫（overrides）、內容清單、與重建注意事項。
> 所有數值皆從線上專案的程式元件原始碼逐一擷取，非估算。

---

## 0. 文件導讀

- 全站幾乎不是用 Framer 原生節點畫的，而是 **把 prototype 的真實 HTML/CSS 1:1 移植進 Framer Code Components**。所以「設計系統」= 程式元件裡的 CSS-in-JS。
- 顏色存在**兩層**並行系統，彼此對應：
  1. **Framer 色彩 token**（有 light/dark 兩組值）— 給原生節點 / 頁面底色用。
  2. **程式元件內部的 CSS `:root` OKLCH 變數**（**只有亮色、沒有深色切換**）— 實際畫面看到的顏色。
- 重建時，§3 設計 token 是地基；§5 全站元件與 §7 逐頁規格是骨架；§8 CMS 與 §9 長文系統是內容引擎。

---

## 1. 品牌與識別

| 項目 | 值 |
|---|---|
| 網站標題（SEO） | `產品經理（Product Manager）作品集｜彭敬鈞（Albert Peng）` |
| 描述（SEO） | `彭敬鈞的產品作品集。兼具產品思維與 AI 落地能力的 PM —— 從需求定義、指標制定到 RAG 架構 POC，完整走過 AI 產品從 0 到上線的每個環節。` |
| 擁有者 | 彭敬鈞 / Albert Peng |
| 角色定位 | 產品經理（Product Manager）｜AI 專案經歷｜產品規劃 |
| 主要語言 | 繁體中文（zh-TW），技術名詞中英混排 |
| 社群分享圖 | `https://framerusercontent.com/images/FeM2HaGJ6LbwCc4vp5yLHIS6mzE.png` |
| Favicon（深） | `https://framerusercontent.com/images/ooEf4swVuAdY70ccX2u8tcyEKxw.png` |
| Apple Touch Icon | `https://framerusercontent.com/images/Fm2oriPrX8PFcy06lyzzU2XEK4.png` |
| 保留 query 參數 | 是（`preserveQueryParams: true`）|

**語氣 / 文案風格**：第一人稱、產品思維、強調「指標」與「落地」；技術名詞用全形括號補充（例：`規則制約（ RULE-BASED ）`）。中文全形標點，括號內前後留半形空格是慣例（`彭敬鈞（ Albert ）`）。

---

## 2. 資訊架構 / 網站地圖

| 路徑 | 頁面 | 由哪個程式元件渲染 |
|---|---|---|
| `/` | 首頁 Home | `AlbertHome` |
| `/about` | 關於 About | `AlbertAbout` |
| `/case-studies` | 精選專案索引（index） | `AlbertWorkHeader` + 原生 CMS list（`WorkCard`）+ `AlbertWorkFooter` |
| `/case-studies/:Case Studies` | 案例詳情（CMS detail） | `CaseDetail` |
| `/blog` | 實作摘錄索引（index） | `AlbertWritingHeader` + 原生 CMS list（`WritingCard`）+ `AlbertWorkFooter` |
| `/blog/:Blog` | 文章詳情（CMS detail） | `PostDetail` |
| `/404` | 404 | `Code404` + `Redirect404`（隱形重導邏輯） |

**舊路徑重導**（由 `Redirect404` 在 404 頁面執行 client-side redirect）：
`/work → /case-studies`、`/project → /blog`、`/writing → /blog`。

> ⚠️ Framer 內部 site-map 的舊名稱（`/project`、`/work`）已過時，實際路徑是 `/blog`、`/case-studies`。

**頁面結構模型**：每一頁 = 套用空的「Main Layout」模板 + `Desktop / Tablet / Phone` 三個 breakpoint frame；每個 breakpoint 內放 1–2 個程式元件實例。索引頁額外插入一個 Framer 原生 CMS collection-list，重複渲染卡片元件。

**Main Layout 模板**（`dY6Cg3xue`）：實質是空殼 —— Desktop breakpoint 寬 1200px、底色 = `BackgroundColor` token、垂直 stack、置中、`overflow:clip`，內部只有一個 `PlaceholderNode`。導覽列、頁尾、聊天鈕都不在模板裡，而在各程式元件內。

### 線上元件 vs. 廢棄草稿
- **線上使用（11 個）**：`AlbertHome`、`AlbertAbout`、`AlbertWorkHeader`、`WorkCard`、`AlbertWorkFooter`、`AlbertWritingHeader`、`WritingCard`、`CaseDetail`、`PostDetail`、`Code404`、`Redirect404`。
- **廢棄舊版（重建時忽略）**：`AlbertHome_1`、`AlbertWork`、`AlbertWork_1`、`AlbertWriting`、`AlbertWriting_1`、`AlbertAbout_1`、`AlbertWorkShell`、`CaseDetail_1`、`CaseDetail_2`、`PostDetail_1`、`PostDetail_2`。

---

## 3. 設計 Token

### 3.1 色彩

實際畫面用的是程式元件 `:root` 的 **OKLCH** 變數（只有亮色）。下表同時給出對應的 Framer token 名稱與 RGB 等值（authoritative）。

| 語意 | CSS 變數（OKLCH 來源） | RGB 亮色 | Framer token | RGB 深色（token 層，程式未實作） |
|---|---|---|---|---|
| 頁面底色 | `--bg` `oklch(0.992 0.004 95)` | `rgb(253,252,249)` | BackgroundColor | `rgb(18,22,30)` |
| 主文字 | `--fg` `oklch(0.225 0.018 262)` | `rgb(23,28,36)` | TextPrimary | `rgb(241,240,236)` |
| 次文字 | `--mfg` `oklch(0.46 0.02 262)` | `rgb(82,88,100)` | TextSecondary | `rgb(147,154,167)` |
| 主色（深靛藍）| `--primary` `oklch(0.325 0.10 262)` | `rgb(21,49,102)` | HighlightColor | `rgb(119,155,221)` |
| 品牌色（青/teal）| `--brand` `oklch(0.605 0.115 200)` | `rgb(0,150,157)` | BrandAccent | `rgb(72,183,189)` |
| 品牌強調 | `--brand-strong` `oklch(0.5 0.12 205)` | `rgb(0,117,131)` | BrandStrong | `rgb(43,166,179)` |
| 卡片底 | `--card` `oklch(1 0 0)` | `rgb(255,255,255)` | Card | `rgb(25,30,38)` |
| 柔和面 | `--muted` `oklch(0.96 0.006 90)` | `rgb(243,242,237)` | Muted | `rgb(34,40,50)` |
| 邊框線 | `--border` `oklch(0.915 0.007 90)` | `rgb(229,227,222)` | Border | `rgb(39,45,55)` |
| 淡色調 | （= 下方 Brand Glow 低透明）| — | AccentTint `rgb(228,239,240)` | `rgb(38,45,57)` |

**Brand Glow（光暈色）**：`oklch(0.665 0.105 200)` ≈ `rgb(72,183,189)`（比 `--brand` 更亮的青）。**未存成變數**，全站以不同透明度反覆使用於：背景光暈、hover 邊框、chip 高亮、bluf 區塊、inline link 底線、focus ring。常見透明度：`/.06 /.09 /.10 /.12 /.18 /.25 /.4`。

**關鍵半透明 / 字面色用法**
- 導覽列底：`oklch(1 0 0/.62)`；頁尾底：`oklch(1 0 0/.5)`；ghost 鈕 / 漢堡鈕底：`oklch(1 0 0/.6)`；左下 badge：`oklch(1 0 0/.78)`。
- 手機選單 `.mob` 底：`oklch(0.99 0.004 95/.9)`（404 為 `/.94`）。
- 頁面背景光暈 `body::before`（fixed, z-index -2）：
  `radial-gradient(55% 45% at 10% -8%, oklch(0.665 0.105 200/.10), transparent 70%), radial-gradient(50% 40% at 94% 4%, oklch(0.325 0.10 262/.07), transparent 70%), var(--bg)`。
- 主色按鈕 `.btn-chat` 漸層：`linear-gradient(180deg, oklch(0.64 0.115 200), oklch(0.54 0.12 205))`，文字 `#fff`。
- `chip.b` 高亮 chip：字 `--brand-strong`，底 `oklch(0.665 0.105 200/.12)`。
- 內文加粗 `.dbody strong`：`oklch(0.27 0.04 262)`（比 `--fg` 略深，一次性字面值）。
- 燈箱遮罩 `.lb`：`oklch(0.18 0.018 262/.84)`。

> 重建若要做深色模式：直接採用上表的 Framer token 深色 RGB，並把程式元件 CSS 的 `:root` 改成依 `prefers-color-scheme` 切換即可（目前程式碼沒有任何深色處理）。

### 3.2 字體與字級

**字族（font stacks）**
- 標題 / UI：`--head: 'Plus Jakarta Sans','Noto Sans TC', sans-serif`
- 內文：`--body: 'Manrope','Noto Sans TC', sans-serif`
- Framer 專案另載入 `Poppins`、`Satoshi`（token 層備用，程式元件未使用）。

**全域基準**：`body` `font-size:17px` / `line-height:1.85` / `letter-spacing:.005em` / `-webkit-font-smoothing:antialiased`。`h1,h2,h3` 一律 `--head` + `letter-spacing:-0.01em` + `text-wrap:pretty`。`html{scroll-behavior:smooth}`。

**OpenType（Framer 文字樣式層）**：標題類啟用 stylistic sets `cv03 cv04 cv09 cv11` + `blwf`（Plus Jakarta Sans 字符變體）。

**型階（實際 CSS，非 Framer preset）**

| 角色 | size | weight | line-height | letter-spacing | 其他 |
|---|---|---|---|---|---|
| Hero H1 `h1.title` | `clamp(42px,5.6vw,76px)` | 800 | 1.06 | -0.025em | max-width 22ch；≤820px → `clamp(26px,7vw,38px)`/1.22 |
| 詳情 Hero `.dhero h1` | `clamp(32px,4vw,52px)` | 800 | 1.12 | — | max-width 24ch |
| 索引頁標 `.page-head h1` | `clamp(32px,3.8vw,50px)` | 800 | — | — | 色 `--primary` |
| 404 標題 `.nf-title` | `clamp(34px,4.6vw,58px)` | 800 | 1.08 | -0.025em | max-width 16ch |
| 區段標 `.sec-head h2` | `clamp(24px,2.6vw,33px)` | 700 | — | — | — |
| About h2（inline）| 30px | 800 | — | — | — |
| 內文區段標 `.dbody .sec-title` | 27px | 700 | — | — | 色 `--primary` |
| 頁尾 h2 | 23px | 700 | — | — | 404 為 21px |
| 引言 `.dbody .ct-q` | 20px | 600 | 1.55 | — | `--head`，左 3px brand 邊 |
| 子標 `.dbody .ct-sub` | 18.5px | 700 | — | — | `--head` |
| About 內文 `.about .bio` | 18px | 400 | 1.95 | — | max-width 62ch |
| 卡片標 `.card h3 / .article h3` | 19px | 700（article 600）| 1.35 | — | — |
| 經歷公司 `.exp .co` | 19px | 700 | — | — | `--head`；small 14px/500 |
| 內文段落 `.dbody p` | 17px | 400 | 1.92 | — | margin 0 0 16px |
| BLUF 文 `.bluf p` | 16.5px | 400 | 1.7 | — | — |
| Logo `.logo` | 16.5px | 700 | — | — | `--head` |
| role-tag / CTA 鈕 | 16.5px / 16px | 500 / 600 | — | — | — |
| 區段副 `.sec-head .sub` | 16px | 400 | 1.6 | — | max-width 52ch |
| 經歷條列 `.exp ul li` | 15.5px | 400 | 1.75 | — | — |
| 詳情 meta 值 `.dmeta b` | 15.5px | — | — | — | `--head` |
| 導覽連結 `.nlinks a` | 15px | 500（active 600）| — | — | — |
| 頁尾連結 `.fcol a` | 15px | — | — | — | — |
| 按鈕 `.btn` | 14.5px | 600 | — | — | `--head` |
| TOC 連結 `.toc a` | 14.5px | 500（active 600）| — | — | — |
| see-all `.seeall` | 14.5px | 600 | — | — | 色 `--primary` |
| 內文格狀說明 `.ct-cell p` | 14.5px | 600 | — | — | `--head`、置中 |
| meta `.meta` | 13.5px | — | — | — | `.co`600 / `.ar`700 |
| 卡片摘要 `.article p` | 14.5px | 400 | 1.65 | — | 3 行截斷 line-clamp |
| more / pn `.more` | 13.5px | 600 | — | — | — |
| 經歷年份 `.exp .yr` | 13.5px | — | — | — | `tabular-nums` |
| copyright `.copy` | 13px | — | — | — | — |
| eyebrow `.overline` | 12.5px | 600 | — | .16em | UPPERCASE，色 `--brand-strong` |
| chip `.chip` | 12px | 500 | — | — | — |
| 標籤 / 日期 `.date / .lab / .dmeta .lab` | 11.5px | 600 | — | .07–.12em | UPPERCASE |

### 3.3 間距與容器

- 容器最大寬 `--maxw: 1440px`；左右留白 `--gut: 52px`（≤1000px → 30px）。
- `.wrap` = `max-width:1440px; margin:0 auto; padding:0 var(--gut)`。
- 導覽列高 70px。
- 一般區段 `section.block` 垂直 padding `60px 0`；區段標題 `.sec-head` margin-bottom 32px。
- Hero padding `104px 0 66px`；CTA margin-top 40px、gap 14px。
- 卡片格 gap 24px；卡片內距 `.cbody` 22px / gap 12px；chip 內距 `5px 11px`、gap 6px。
- 詳情閱讀欄 `.dbody` max-width **1000px**；TOC 欄寬 **220px**；`.dlayout` grid `220px 1fr` gap 56px；TOC `sticky top:96px`；段落 `scroll-margin-top:96px`。
- 頁尾 padding `60px 0 84px`、`.fnav` gap 56px。
- 浮動元素：聊天鈕 `right:24px; bottom:24px`；badge `left:14px; bottom:14px`；燈箱 padding 40px。

### 3.4 圓角

| Token / 值 | 用於 |
|---|---|
| `--rc: 20px` | 卡片、`.dcover`、`.nf-card` |
| `--rl: 16px` | `.bluf`、`.figure` |
| `999px`（pill）| 導覽連結、`.btn`、`.chip`、聊天鈕、badge、`.bluf .k` |
| `24px` | About 人像 `.about .photo` |
| `12px` | 漢堡鈕、燈箱圖 |
| `11px` | 404 卡片 icon |
| `8px` | `.figure img`（外加 `clip-path:inset(3px round 6px)`，僅 PostDetail）|
| `2px` | 漢堡線條 |
| `50%` | logo 圓點、條列項目圓點 |

### 3.5 陰影 / 高度

| Token | 值 | 用於 |
|---|---|---|
| `--sh-sm` | `0 1px 3px oklch(0.225 0.018 262/.06), 0 1px 2px oklch(0.225 0.018 262/.05)` | 導覽列、卡片靜態、figure |
| `--sh-md` | `0 14px 36px oklch(0.225 0.018 262/.10)` | `.dcover`、figure hover、人像（404 省略此 token）|
| `--sh-lg` | `0 28px 60px oklch(0.225 0.018 262/.14)` | 卡片 hover（詳情頁定義但未用）|
| 聊天鈕 | `0 10px 24px oklch(0.55 0.12 205/.3), inset 0 1px 0 oklch(1 0 0/.25)` | `.btn-chat` |
| 浮動聊天 | `0 14px 30px oklch(0.55 0.12 205/.4)` | `.chat` |
| logo ring | `0 0 0 4px oklch(0.665 0.105 200/.18)` | 圓點外光 |
| 燈箱圖 | `0 30px 80px rgba(0,0,0,.5)` | `.lb img` |

**Backdrop blur**：導覽列 `blur(16px) saturate(140%)`；手機選單 `blur(20px)`；頁尾 / ghost 鈕 / 燈箱 `blur(8px)`。

### 3.6 Z-index 層級

`body::before` 背景光暈 `-2` → 浮動聊天 / badge `60` → 導覽列 `50` → 手機選單 `48` → 燈箱 `100`。

### 3.7 動效

- **標準緩動**：`cubic-bezier(.2,0,0,1)`（卡片、手機選單、reveal 動畫共用）。
- **過場時長**：導覽連結 `.18s`、按鈕/see-all/TOC/figure `.2s`、卡片 `.28s`、縮圖圖片 `.4s`、手機選單 `.32s`。
- **hover**：聊天鈕 `translateY(-2px)`；卡片 `translateY(-6px)` + 縮圖 `scale(1.05)` + 邊框轉 Brand Glow `/.4`；see-all gap `7px→11px`（箭頭外滑）+ 底線轉 brand；figure hover 顯示 `.zhint` 提示。
- **進場 reveal**：`@keyframes rise{to{opacity:1;transform:none}}`，`.rv{opacity:0;transform:translateY(14px);animation:rise .6s cubic-bezier(.2,0,0,1) forwards}`；錯位延遲 `.d1=.04s / .d2=.1s / .d3=.17s`。
- 全站尊重 `@media(prefers-reduced-motion:reduce)`（關閉 reveal）。404 頁無 reveal 動畫。

### 3.8 斷點（Breakpoints）

存在**三套**斷點，重建時要分清：

1. **Framer 頁面 breakpoint**（畫布層）：Desktop 1200px / Tablet 810px / Phone 390px。
2. **CSS media query**（首頁、關於、索引、404 等以 viewport 為準）：
   - `@media(min-width:821px)`：隱藏手機選單 `.mob`。
   - `@media(max-width:1000px)`：`--gut` 30px；卡片格 3→2 欄；About / Experience → 1 欄；TOC 轉水平捲動。
   - `@media(max-width:820px)`：隱藏桌面導覽、顯示漢堡；所有格 → 1 欄；Hero 標題縮小；區段標題改直排。
3. **ResizeObserver（容器寬）**：**僅詳情頁** `CaseDetail` / `PostDetail` 用元件實際寬度切換 `.rsp-narrow`（≤1000）/ `.rsp-phone`（≤820），不靠 viewport media query（因為元件嵌在 Framer 容器內）。

---

## 4. 版面系統

- 主結構：置中容器（`max-width:1440px` + 52px 左右留白），偏 **Centered container layout**。
- 卡片區用 3 欄 grid（`repeat(3,1fr)` gap 24px）→ 2 欄（≤1000）→ 1 欄（≤820）。
- 詳情頁用 **sidebar layout**：左 220px sticky TOC + 右 1000px 閱讀欄（gap 56px）。
- Experience 用三欄 grid `220px 1fr auto`（公司 / 條列 / 年份）。
- About 用兩欄 `320px 1fr`（人像 / 文字 + 技能）。

---

## 5. 全站共用元件

### 5.1 導覽列 Navigation（sticky glass nav）

- `position:sticky; top:0; z-index:50`；高 70px；底 `oklch(1 0 0/.62)` + `backdrop-filter:blur(16px) saturate(140%)`；底邊 `1px solid oklch(1 0 0/.6)`（404 用 `--border`）；陰影 `--sh-sm`。
- **左側 Logo**：`<span class="dot">`（9×9px brand 圓點 + 外光 ring）+ 文字 `彭敬鈞（ Albert ）`，連到 `/`。
- **中間連結** `.nlinks`（pill，內距 `9px 16px`，gap 4px）：
  - `首頁` → `/`
  - `精選專案` → `/case-studies`
  - `實作摘錄` → `/blog`
  - `關於` → `/about`
  - `聯絡` → `/#contact`
  - hover：底 `oklch(0.665 0.105 200/.10)`；`.active`：字 `--primary`、底 `oklch(0.325 0.10 262/.07)`、weight 600。
- **右側按鈕** `.btn-out`：`履歷 Resume` → `https://www.cake.me/albert-peng`（`target=_blank`，外部箭頭 SVG）。邊框 `1.5px solid oklch(0.325 0.10 262/.25)`，hover 底 `oklch(0.325 0.10 262/.06)`。
- **active 狀態為硬寫**（各頁的 HTML 直接給對應連結 `class="active"`），非 JS 計算。連結帶 `data-v="home|work|writing|about|contact"`。

**手機選單 `.mob`（漢堡抽屜）**
- 漢堡鈕 `.burger`（46×46，圓角 12，3 條 21×2px bar），`≤820px` 顯示。
- `.mob`：`position:fixed; inset:0; z-index:48`，底 `oklch(0.99 0.004 95/.9)` + `blur(20px)`，padding `94px var(--gut) 40px`，連結 27px/600。
- 行為（`useEffect`）：點漢堡 → `body.classList.toggle("menu")`（首頁/關於/索引）或 `root.classList.toggle("menu")`（詳情頁）；點任一 `.mob a` → 移除 `menu`。`.menu` 時 `.mob` 由 `translateY(-100%)` 滑入、`overflow:hidden`。`≥821px` 強制 `.mob{display:none}`。404 另監聽 `matchMedia("(min-width:821px)")` 在放大時自動關閉選單。

### 5.2 頁尾 Footer

- `id="contact"`（即 `/#contact` 錨點目標）；底 `oklch(1 0 0/.5)` + `blur(8px)`；上邊 `1px solid var(--border)`；padding `60px 0 84px`。
- 結構：左欄品牌（h2 + 副述 + 聊天 CTA）+ 右側兩欄連結 `.fnav`（gap 56px）+ 底部 copyright。
- **h2**：`彭敬鈞（ Albert Peng ）`
- **副述 `.fsub`**：`產品經理（ PRODUCT MANAGER ）｜AI 專案經歷｜產品規劃。專注於將複雜的 AI 技術轉化為解決實際痛點的優質產品。`
- **聊天 CTA `.btn-chat`**：`✦ 瞭解 彭敬鈞（ Albert ）`（icon `✦` U+2726，16px span）。
- **欄 1（label `導覽`）**：`精選專案`/`/case-studies`、`實作摘錄`/`/blog`、`關於我`/`/about`。
- **欄 2（label `Social`）**：`LinkedIn`（`https://www.linkedin.com/in/albertpeng1227`）、`Email`（`mailto:albertpeng678@gmail.com`）、`履歷 Resume`（cake.me）。每條帶外部箭頭 SVG。
- **Copyright**：`© 2026 – Albert Peng @ Copyright`。
- 404 頁尾為簡化版：h2 `彭敬鈞（ Albert ）`、副述 `兼具產品思維與 AI 落地能力的產品經理。`、欄 2 label 改 `Connect`、無 copyright、無聊天鈕。

> 詳情頁的聊天 CTA 帶 class `.foot-chat-cta`，點擊會 `preventDefault` 並觸發全站 widget（見 §10）；首頁/關於/索引的聊天鈕為裸 `<a class="btn btn-chat">`（無 href、無 inline handler），靠 §10 的 override 接管。

### 5.3 全站 AI 聊天 Widget（「來聊聊」/ Albert bot）

- 期望頁面上有一個 `id="albert-widget"` 的 `<iframe>`（全站聊天機器人載體，本身在 Framer 畫布全域層，不在這些程式元件內）。
- 觸發機制（統一）：`document.getElementById("albert-widget").contentWindow.postMessage({ type: "open-widget" }, "*")`。
  - **訊息 payload**：`{ type: "open-widget" }`；**targetOrigin**：`"*"`。
- 兩種接線方式：(a) 詳情頁在 `useEffect` 內對 `.foot-chat-cta` 綁定；(b) 其他頁靠 Framer override `withOpenAlbertWidget`（§10）綁在按鈕上。

### 5.4 燈箱 Lightbox

- 標記 `<div class="lb" id="lb"><span class="x">✕</span><img id="lbimg"></div>`。
- `position:fixed; inset:0; z-index:100`；遮罩 `oklch(0.18 0.018 262/.84)` + `blur(8px)`；圖 `max-width:96vw; max-height:92vh`、圓角 12、陰影 `0 30px 80px rgba(0,0,0,.5)`；關閉鈕 `.x` 32px 白色於 `top:20px right:26px`。
- 顯示 = 加 `.on`（`display:flex`）。**詳情頁**才有開關 JS：點 `.figure` → 設 `#lbimg` src + 加 `.on`；點圖以外處關閉。

### 5.5 共用 UI 基元

- **按鈕**：`.btn`（pill，`--head`/600/14.5px，內距 `11px 20px`）；變體 `.btn-out`（描邊主色）、`.btn-chat`（青色漸層、白字、hover 上移）、`.btn-ghost`（白玻璃底）。CTA 變體加大內距 `15px 28px`、字 16px。
- **chip / 標籤**：pill，12px/500，底 `--muted`、字 `--mfg`；首個 chip 用 `.chip.b`（字 `--brand-strong`、底 Brand Glow `/.12`）。
- **overline / eyebrow**：12.5px/600、`.16em`、UPPERCASE、`--brand-strong`。
- **meta 列**：`{公司} · {年份} →`（中點 U+00B7 + 箭頭 →）；公司 600/`--fg`、年份 700/`--brand-strong`。

---

## 6. 卡片元件

### 6.1 Work Card（案例卡，`WorkCard.tsx`）
- 結構：`.card`（flex 直排、`height:100%`、`overflow:hidden`）→ `.thumb`（`aspect-ratio:16/10`、底 `--muted`）+ `.cbody`（h3 + `.chips` + `.meta`）。
- 樣式：圓角 `--rc`（20px）、邊框 `1px var(--border)`、陰影 `--sh-sm`；hover 上移 6px + 陰影 `--sh-lg` + 邊框 Brand Glow `/.4`；縮圖 hover `scale(1.05)`。
- Framer property controls：`title`、`tags`（全形 `｜` 分隔，首個 → `chip b`）、`company`、`year`、`thumb`。
- meta 格式：`{company} · {year} →`。

### 6.2 Writing Card（文章卡，`WritingCard.tsx`）
- 結構同 `.article`：`.thumb` + `.cbody`（`.date`?、h3、`p`、`.more`）。
- h3 19px/600；摘要 `p` 14.5px/1.65、**3 行截斷**（`-webkit-line-clamp:3`）；`.more` 固定文字 `閱讀摘錄 →`（U+2192）。
- 日期格式化 `fmtDate`：ISO `YYYY-MM-DD` → `YYYY · MM · DD`（中點 U+00B7）；空字串則不顯示日期列。
- Framer controls：`title`、`date`、`excerpt`、`thumb`。
- 卡片本身無 `<a>`，連結由 Framer CMS list 包覆層提供。

---

## 7. 逐頁規格

### 7.1 首頁 `/`（`AlbertHome`）
由上到下：sticky nav → Hero → 「Selected Work」3 卡 → 「Writing」3 文（位於 `.writing-bleed` 淡青漸層帶）→ 「Experience」時間軸 → 「About」兩欄（人像 + bio + 技能）→ footer。附隱形燈箱標記（首頁不啟用）。

- **Hero**：overline `彭敬鈞 · Albert · Product Manager`；H1 `收斂定義對的問題`（換行）`交付符合需求場景的體驗`；role-tag `產品經理（ Product Manager ）｜AI 專案經歷｜產品規劃`；CTA `✦ 瞭解 彭敬鈞（ Albert ）` + `履歷 Resume`。
- **Selected Work**：overline `Selected Work`、h2 `精選專案`、sub `以產品指標思維，進行 AI 應用落地與效果驗證`、see-all `看全部專案（5）→`。3 張卡片（見 §8 內容）。
- **Writing**：overline `Writing`、h2 `實作摘錄`、sub `個人運用 AI 所學落地的 side project，以及其他專案記錄`、see-all `看全部摘錄（3）→`。
- **Experience**：overline `Experience`、h2 `工作經歷`（內容見 §11）。
- **About**：overline `About · 關於我`、h2 `I'm Albert（ 彭敬鈞 ）`、bio 段、4 組技能分類（見 §11）。
- 行為：僅漢堡選單；reveal 動畫純 CSS；無 IntersectionObserver。

> ⚠️ 首頁/關於頁的程式元件「夾帶整份全站 CSS」（含詳情頁 `.dhero/.dlayout/.toc/.dbody/.bluf/.figure/.ct-grid/.prevnext/.chat/.badge/.lb` 樣式，雖然該頁不用）。**重建時把首頁/關於頁視為完整 token 集的標準來源。**

### 7.2 關於 `/about`（`AlbertAbout`）
CSS 與首頁 byte-identical，HTML 不同：nav → `.page-head`（overline `About` + H1 `關於我`）→ 與首頁相同的 About 區塊（人像 + bio + 4 技能分類）→ footer。導覽 active 移到 `關於`。

### 7.3 精選專案索引 `/case-studies`
組成：`AlbertWorkHeader`（nav + page-head）+ 原生 CMS list（重複 `WorkCard`，來源 collection `Case Studies`）+ `AlbertWorkFooter`。
- page-head：overline `Selected Work`、H1 `精選專案`、sub `以產品指標思維，進行 AI 應用落地與效果驗證`。
- 卡片格 `.grid-work` 3 欄。Header 只渲染 `PRE` 切片（grid 之前），卡片由 Framer CMS list 注入。

### 7.4 案例詳情 `/case-studies/:Case Studies`（`CaseDetail`）
版面：nav → `.dhero`（back link、tag chips、H1、`.dmeta` COMPANY/ROLE/YEAR）→ `.dcover`（封面圖）→ `.bluf`（重點摘要）→ `.dlayout`（220px sticky TOC + 1000px 內文）→ `.prevnext` → footer → 燈箱。
- 消費 CMS 欄位：`title`、`company`、`role`、`year`、`expertise`（逗號分隔 chip，首個 `.chip.b`）、`heroURL`、`bLUF`、`tOCJSON`（JSON → TOC）、`sectionHTML`（內文 HTML）、`prevSlug/prevTitle`、`nextSlug/nextTitle`。（`tagline` 有宣告但未渲染 = 死欄位。）
- 固定文案：back `← 精選專案`、meta 標 `COMPANY`/`ROLE`/`YEAR`、BLUF 標 `重點 BLUF`、TOC 標 `ON THIS PAGE`、`← PREV`/`NEXT →`。
- 行為：漢堡選單、聊天 `.foot-chat-cta`、**TOC scroll-spy**（IntersectionObserver、`rootMargin:"-80px 0px -60% 0px"`、加 `.on`）、**圖片燈箱**、`ResizeObserver` 響應式。

### 7.5 實作摘錄索引 `/blog`
組成：`AlbertWritingHeader`（nav + page-head）+ 原生 CMS list（重複 `WritingCard`，來源 collection `Blog`）+ `AlbertWorkFooter`。
- page-head：overline `Writing`、H1 `實作摘錄`、sub `個人運用 AI 所學落地的 side project，以及其他專案記錄`。
- 卡片格 `.grid3` 3 欄。

### 7.6 文章詳情 `/blog/:Blog`（`PostDetail`）
結構與 `CaseDetail` 幾乎相同（root class `.pd-root`）。差異：
- Hero 較簡（無 tag chips、無 COMPANY/ROLE/YEAR）：只有 title + `DATE`（格式化 `YYYY · MM · DD`）。
- 封面欄位名為 `imageURL`（非 `heroURL`）。
- back link `← 實作摘錄`；prev/next 指向 `/blog/{slug}`；導覽 active 在 `實作摘錄`。
- 唯一樣式差異：`.figure img` 多 `clip-path:inset(3px round 6px)`。
- 消費 CMS 欄位：`title`、`date`、`imageURL`、`bLUF`、`tOCJSON`、`sectionHTML`、`prevSlug/prevTitle`、`nextSlug/nextTitle`。

### 7.7 404 `/404`（`Code404` + `Redirect404`）
- 版面：nav → 置中 `.nf`（overline `Error 404 — Page not found`、標題 `這個頁面好像迷路了…`、副述、兩個 CTA、3 張連結卡）→ 簡化 footer。
- CSS 為主系統的精簡變體：移除卡片/文章/經歷/about/詳情/聊天/燈箱樣式，新增 `.nf-*`；省略 `--sh-md`；背景光暈更強；無 reveal 動畫。
- CTA：`返回首頁`（`/`，btn-chat + 返回箭頭 SVG）、`瀏覽精選專案`（`/case-studies`，btn-ghost）。
- 連結卡：`精選專案`/`/case-studies`、`實作摘錄`/`/blog`、`關於我`/`/about`，各帶 `前往` + Lucide 風 SVG icon。
- `Redirect404`：隱形 1×1，client-side 重導（見 §2）。`useIsStaticRenderer` 在編輯器/SSR 時 no-op；保留 query + hash，用 `location.replace`。

---

## 8. CMS 資料模型

兩個 collection。詳情頁直接讀「pre-rendered」欄位（`detailHTML` / `secHTMLStr` / `tocJSON` 等），即內容是事先做好的 HTML 字串（由作者/Claude 產出），metadata 在 CMS 可編輯。

### 8.1 Collection：Case Studies（5 筆）
欄位：`Title`(string)、`Slug`(string, 自動)、`SEO Description`(string)、`Company`(string)、`Role`(string)、`Year`(string)、`Expertise`(string, 逗號分隔)、`Hero Image`/`heroURL`(string/image)、`BLUF`/`blufText`(string)、`TOC JSON`/`tocJSON`(string)、`Detail HTML`/`detailHTML`(richtext)、`secHTMLStr`(string)、`prevSlug`/`prevTitle`、`nextSlug`/`nextTitle`(string)、`id`(string)。

| Title | Slug |
|---|---|
| AI Search for KM - 產品路線 | `product-roadmap` |
| AI Search for KM - 問答架構重構 | `qa-re-construct` |
| 知識圖譜檢索（ Graph RAG ）驗證 | `knowledge-graph` |
| 自然語言生成 SQL 查詢（ NL2SQL ）驗證 | `nl2sql` |
| AI 掃描新增履歷 - PDF 履歷匯入 | `ai-scanning` |

首頁卡片對應縮圖：`product-roadmap`=`pLPFG43VvaWDaJkv5zwDvfRGA.png`、`qa-re-construct`=`EoTgOabMVl6jFTLUC4uchPPUA.png`、`knowledge-graph`=`hUxgCU9QCdQSg6ryglsUUdXw1oI.png`、`nl2sql`=`Fq0Y8NmdnQXf1nRe6bIpmNVzU.png`、`ai-scanning`=`o5LRV8NoEt9YLwlD6zCygVDSLdw.png`（皆 framerusercontent.com/images/）。

### 8.2 Collection：Blog（3 筆）
欄位：`Title`、`Slug`、`SEO Description`、`Date`(date)、`Image`(image)/`Image URL`(string)、`Content`(richtext)、`BLUF`/`blufText`、`TOC JSON`/`tocJSON`、`Detail HTML`/`detailHTML`(richtext)、`secHTMLStr`、`prevSlug`/`prevTitle`、`nextSlug`/`nextTitle`、`id`。

| Title | Slug | 縮圖 |
|---|---|---|
| Portfolio AI Bot：讓作品集開口說話 | `portfolio-ai-bot` | `rnykDN4l5PCng7HKYHQFVjPTOSE.png` |
| 台灣金融法規 AI 問答系統：讓 2,695 條金融法規開口說話，每個答案都有條文出處可追溯 | `ais-law-rag` | `g76iyVz4cnSxFVmyMKRbx7Cdw.png` |
| 104 實習平台系列：從學生真實痛點出發，打造無雜訊的專屬求職體驗 | `104-intern-platform` | `VKWkEgrzvjQgk3L0zFiRpxD5Hcc.webp` |

> 重建建議：collection 仍存「可編輯 metadata（標題/slug/日期/封面/SEO/prev-next）」+「pre-rendered 內文（`sectionHTML`/`tocJSON`/`bLUF`）」的分工。內文用 §9 的 class-based 結構撰寫。

---

## 9. 長文（內文）排版系統 — class-based

詳情頁的內文 `sectionHTML` **不靠 HTML 標籤自動套樣式，而是靠特定 class**。裸 `h4/h5/h6/ul/ol/code/pre/em/blockquote/figcaption` 無樣式 —— 撰寫內文時必須用下列 class：

| Class | 用途 | 樣式重點 |
|---|---|---|
| `.sec` | 區段容器（TOC 錨點）| `padding-bottom:52px; scroll-margin-top:96px`；需設 `id` 對應 TOC |
| `.sec-title` | 區段標題（≈h2）| 27px/700、色 `--primary`、mb 18px |
| `p` | 段落 | 17px/1.92、`margin:0 0 16px` |
| `strong` | 加粗 | 700、色 `oklch(0.27 0.04 262)` |
| `.ct-sub` | 子標題 | 18.5px/700、`--head`、`margin:26px 0 10px` |
| `.ct-q` | 引言/區塊引述 | 20px/600、`--head`、左 `3px solid var(--brand)`、`padding:4px 0 4px 24px`；`strong` 轉 `--brand-strong` |
| `.ct-list` + `>li` | 自訂條列 | `list-style:none`、gap 12px、li 16.5px/1.8、左 24px、`::before` 7px 青點 |
| `.ilink` | 內文連結 | 色 `--brand-strong`、底線色 Brand Glow `/.4`、`underline-offset:3px`、600 |
| `.figure` | 圖片框 | 圓角 `--rl`、邊框、`--sh-sm`、padding 14px、`cursor:zoom-in`（點開燈箱）；img max-height 440px、圓角 8 |
| `.figure .zhint` | 圖片提示 pill | 11.5px、底 `oklch(0.225 0.018 262/.78)`、hover 顯示 |
| `.ct-grid` | 圖文格 | `repeat(var(--cols,2),minmax(0,1fr))` gap 20px；`.ct-cell` 內 img max-height 300px、說明 14.5px/600 置中 |

**TOC**：`tocJSON` = `[{id,label}]` → 渲染成 `<a href="#id">label</a>`；scroll-spy 用 IntersectionObserver 在對應 `.sec` 進入視窗時把該 TOC 連結加 `.on`（字 `--brand-strong`、左框 `--brand`）。`id` 需與 `sectionHTML` 內 `.sec` 的 `id` 一致（元件不自動產生 id）。

**BLUF 區塊** `.bluf`：青色漸層底 + Brand Glow `/.25` 邊；標籤 `.bluf .k`（pill、白字、底 `--brand-strong`）顯示 `重點 BLUF`；內文 16.5px/1.7。

**prev/next** `.prevnext`：上邊框分隔，左 `← PREV` / 右 `NEXT →`（`.pn` 15px/600、small 標籤 11.5px UPPERCASE），最大寬各 46%。

---

## 10. 程式覆寫 Code Overrides

| Override | 來源檔 | 作用 |
|---|---|---|
| `withOpenAlbertWidget` | `Examples.tsx` | **聊天 widget 觸發器**。`onClick`：`event.preventDefault()` → 串接既有 `props.onClick` → SSR guard → `document.getElementById("albert-widget")` 取 iframe → `iframe.contentWindow.postMessage({ type:"open-widget" }, "*")`。綁在聊天按鈕上即可開啟全站 bot。 |
| `withRichTextImages`（`RichTextImages.tsx`）| 把 rich-text 圖片強制 `width:100%`（滿欄）。 |
| `withRotate` | `Examples.tsx` | demo：`animate={{rotate:90}}`, `duration:2`。 |
| `withHover` | `Examples.tsx` | demo：`whileHover={{scale:1.05}}`。 |
| `withRandomColor` | `Examples.tsx` | demo：共享 store（初始 `#0099FF`），點擊換隨機色。 |

`Examples.tsx` 匯入 `createStore`（framer store）與 `randomColor`（framer utils）。`withRotate/withHover/withRandomColor` 是 Framer 範例覆寫，與作品集設計無關，可忽略。

---

## 11. 內容清單（重建可直接沿用）

### 導覽 / 頁尾 / 社群連結
- Resume：`https://www.cake.me/albert-peng`
- LinkedIn：`https://www.linkedin.com/in/albertpeng1227`（註：`CaseDetail` 內出現過另一寫法 `https://www.linkedin.com/in/albert-peng-pm/` — 重建請統一，建議以 `albertpeng1227` 為準或向本人確認）
- Email：`albertpeng678@gmail.com`

### 首頁 Experience（工作經歷）
| 公司 | 職稱 | 期間 | 重點 |
|---|---|---|---|
| 意藍資訊 | 產品經理（ Product Manager ） | 2025.04 – 現今 | 建 RAG 產品指標體系；有效提問覆蓋率 68% → 逾 85%；降低 90% 提示注入風險 |
| 104 人力銀行 | 產品管理實習生 | 2024.01 – 2024.08 | 實習平台 0→1；Looker Studio；7 份國內外競品分析；AI 掃描 LinkedIn 匯入 |
| 碩網資訊 | 專案助理實習生 | 2023.06 – 2023.12 | 4 個大型 B 端客戶 AI 客服；70% 功能規格書；客房服務系統網站主負責人 |

### 技能分類（About）
- **AI 產品架構與概念驗證**：RAG、GraphRAG、NL2SQL、AI Agent、提示工程、上下文工程、Claude Code、Google Antigravity、Mermaid、Draw.io
- **數據驅動與指標評估**：AI Eval、產品指標制定、GA4、GTM、Looker Studio、SQL、ETL
- **產品管理與團隊協作**：敏捷開發、Scrum、Jira、Trello、Redmine、Confluence、Notion、Markdown
- **產品探索與體驗設計**：Figma、Axure RP、Hotjar、UI／UX、需求訪談、競品分析

### Bio（About / 首頁）
標題 `I'm Albert（ 彭敬鈞 ）`；內文以「具備 B 端與 C 端… 轉化為解決實際痛點的優質產品。」開頭。

---

## 12. 圖示與資產

- **外部連結箭頭**（取代 ↗ emoji，避免 iOS 彩色 emoji）：inline SVG `viewBox='0 0 10 10' stroke='currentColor' stroke-width='1.4'`，內含 `<line x1='2.6' y1='7.4' x2='7.4' y2='2.6'/>` + `<polyline points='3.6 2.6 7.4 2.6 7.4 6.4'/>`，尺寸 `0.72em`。
- **字符 glyph**：`✦`(U+2726 聊天鈕)、`◎`(U+25CE 經歷條列點)、`→`(U+2192)、`←`、`✕`(U+2715 燈箱關閉)、`·`(U+00B7 日期/meta 分隔)。
- **404 icon**：5 個 Lucide 風 24×24 SVG（返回箭頭、2×2 grid、open-book、user、右箭頭）。
- **人像**：`3I8IwlSSsiWC2Gt9cj1qNJuaQAc.jpeg`。
- 縮圖見 §8；皆 `loading="lazy"`、`aspect-ratio:16/10`、`object-fit:cover`。
- 內部圓點（logo dot、條列點、技能點）皆 CSS，不是 SVG。

---

## 13. 重建注意事項 / 決策紀錄

1. **1:1 移植，不要重畫原生節點**：設計細節（OKLCH 色、stylistic sets、clamp 字級、scroll-spy）只能靠程式元件保真，用 Framer 原生節點重畫會失真。
2. **兩層色彩要對齊**：程式 `:root` OKLCH（亮色）↔ Framer token（light/dark）已一一對應（見 §3.1）。若要新增深色模式，補 `prefers-color-scheme` 並沿用 token 深色值。
3. **斷點三套並存**：詳情頁用 ResizeObserver（因嵌在容器內，viewport media query 不準），其餘頁用 viewport media query；別混用。
4. **內文是 class-based**：CMS 內文必須用 §9 的 class，否則無樣式。
5. **聊天 bot 是全域 iframe**（`id="albert-widget"`）+ `postMessage({type:"open-widget"})`；不要在頁面元件內重複放 widget，只放觸發按鈕。
6. **詳情頁 = CMS 驅動**：標題/日期/封面/SEO/prev-next 為可編輯 metadata；內文為 pre-rendered HTML（`sectionHTML`）+ `tocJSON` + `bLUF`。
7. **CSS 重複**：卡片樣式在多檔重複定義（值相同）；header/footer 檔各自夾帶整份 stylesheet。重建時抽成單一共用 stylesheet 較佳。
8. **清掉廢棄草稿**：`_1`/`_2`/`AlbertWork`/`AlbertWriting`/`AlbertWorkShell` 為舊版，重建忽略。
9. **已知小瑕疵**：`tagline`（Case）為死欄位；`--sh-lg`（詳情頁）定義未用；LinkedIn 連結兩種寫法需統一。
10. **聊天鈕兩種接線**：詳情頁用 `.foot-chat-cta` + `useEffect`；其餘頁用 `withOpenAlbertWidget` override —— 重建建議統一成一種。

---

*本文件由實際線上 Framer 專案（project `cvsGflMU4eamAt4g8jKz`）原始碼擷取生成，數值可作為重建的權威依據。*
