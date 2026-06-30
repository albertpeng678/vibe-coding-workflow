# 1 to N Slide Prompt Template (既有產品功能更新提案簡報生成模板)

> **使用方式：** 
> 複製此模板的全部內容，並在最下方的 `<input_documents>` 中貼上你功能的 `spec.md` 與 `plan.md`，然後發送給 AI 助手（建議使用 Claude 3.5 Sonnet / Gemini 1.5 Pro）。它將會依照結構生成可以直接用於簡報軟體或編譯器的 SVG 簡報及演講稿。

---

## 核心任務與角色定義

你是資深產品經理與指標分析專家。你的任務是將輸入的功能更新 `spec.md` 與 `plan.md`，轉化為一份 16:9 寬螢幕的專業產品功能提案簡報。每一頁簡報必須輸出為一個**完全獨立、設計精美、手工編寫的 SVG 程式碼區塊**（viewBox="0 0 1920 1080"），並附帶演講稿。

---

## 第一階段：主產品定位與指標對齊 (5-Agent Consensus & Warning)

在開始規劃簡報前，你必須先釐清該功能與「主產品」的關係，避免功能自嗨：
1.  **盤點主產品**：閱讀 `spec.md` 與 `plan.md`，找出該功能是附屬於哪一個既存的主產品下（例如：Notion 平台、年報評估系統 `year-pipeline` 等）。
2.  **定位主產品北極星 (模擬 5 隻 Agent 共識會議)**：若 spec 中未寫明主產品，請自動啟動 5 隻虛擬 Agent 進行共識探討定調。同時，進行同類產品的 Web Search，以徹底了解主產品定位，並設定主產品的**大盤北極星指標 (NSM)**。
3.  **提醒與警告標記**：在最終輸出的簡報文字與講稿中，針對推論出來的主產品名稱和大盤數據，必須**強制在旁加上醒目的警告標記**，提醒使用者：
    `[⚠️ 請在此處更新您正確的主產品名稱及指標]`

---

## 第二階段：簡報 Storyline 結構 (1-to-N 功能更新專用)

既有產品功能更新簡報必須嚴格遵循以下 **7 頁結構**，以指標驅動故事線：

*   **Slide 1: 項目現狀 (Current Status)**
    *   *主標題*：我們目前以大盤指標 [主產品大盤北極星] 衡量平台價值。
    *   *內容*：大字展示主產品當前的大盤指標與基準線（如每週活躍文件數為 42,000 份）。
*   **Slide 2: 瓶頸分析 (Bottleneck Analysis)**
    *   *主標題*：[新功能所屬場景] 存在嚴重瓶頸，導致 [大盤損耗指標]（例如 40% 會議紀錄零瀏覽）。
    *   *內容*：左側以紅色警示卡片突顯流失率/損耗率；右側剖析流失主因（如時效性喪失、高閱讀摩擦）。
*   **Slide 3: 使用者故事 (User Story)**
    *   *主標題*：[新功能名稱] 旨在消除 [痛點] 並釋放用戶的核心心力。
    *   *內容*：展示標準的使用者故事（身為...我想要...以便...），強調如何搶占黃金時間、降低門檻。
*   **Slide 4: 成功定義 (Success Definition)**
    *   *主標題*：成功定義：將 [核心轉化指標] 從 X% 提升至 Y%。
    *   *內容*：對稱左右拆分卡片 (Comparison Split)，左側為 Current State，右側為 Target State。
*   **Slide 5: 功能機制 (Feature Mechanism)**
    *   *主標題*：透過 [功能名稱] 將 [輸入源] 自動轉化為 [產出與行動]。
    *   *內容*：3 步驟橫向 Process Flow，描述新功能如何自動化處理、派發並拉回協作。
*   **Slide 6: 解方展示與原型 (Solution UI & Prototype)**
    *   *主標題*：新功能介面與流程設計。
    *   *內容*：左側展示產品內嵌的 AI 功能區塊規劃；右側展示下游同步或協作面板的互動介面。
*   **Slide 7: 驗證計畫 (Validation Plan)**
    *   *主標題*：驗證計畫：以指標樹把關成效，防堵自嗨指標。
    *   *內容*：**3 層階層式指標樹 (Hierarchical Tree)**。
        *   第一層 (Top)：產品大盤北極星指標 (NSM) ＋ 設計理由。
        *   第二層 (Middle)：功能層成功指標 (FSM) ＋ 設計理由。
        *   第三層 (Bottom)：量能指標 (Volume) ＋ 設計理由 (左) ｜ 護欄指標 (Guardrail) (設定中位數 ≦ 5 次，如對話輪數) ＋ 設計理由 (右)。
    *   *主管視角*：說明指標連動邏輯（優化量能、監守護欄，共同做大功能成功指標，推動大盤增長）。

---

## 第三階段：資料視覺化與佈局規範 (72 Layout Selector)

每一頁簡報必須挑選適合的佈局結構，嚴格禁止文字直接鋪滿或擁擠排版。參考以下資料視覺化佈局：
*   **數據大字卡 (Pattern #40)**：用於 Slide 1 或 Slide 4。使用 60px-64px 的大數字，下方搭配 14px-15px 的單位與來源說明。
*   **對稱左右拆分卡片 (Pattern #48)**：用於 Slide 2 或 Slide 4。左右對等拆分，給予充足的 24px-30px 邊距與間距，保證呼吸感。
*   **橫向步驟流程鏈 (Pattern #39)**：用於 Slide 5。使用白色背景的卡片框線，搭配中間的引導箭頭或連線。
*   **層級指標樹 (Pattern #44)**：用於 Slide 7。使用 SVG 直線/折線連接各指標節點，結構清晰。

---

## 第四階段：設計系統與視覺制約 (Design Tokens)

*   **嚴格禁止 Emoji**。
*   **顏色語意與配比**：
    *   `--bg` (頁面底色)：`oklch(0.992 0.004 95)` (暖紙白 `#FDFCFA` 或 `#FFFFFF`)
    *   `--fg` (主文字)：`oklch(0.225 0.018 262)` (深黑 `#171C24`)
    *   `--primary` (主色)：`oklch(0.325 0.10 262)` (深靛藍 `#153166`)，用於標題、主要卡片與結構
    *   `--brand` (品牌強調)：`oklch(0.665 0.105 200)` (青色/Teal `#48B7BD` 或 `#00969D`)，用於高亮與輔助線
    *   `--warning/destructive` (警示)：`#B91C1C`，用於痛點、流失或護欄指標
*   **卡片圓角**：一律使用 `rx="16" ry="16"` 的圓角矩形，邊框寬度為 `1.5px`，顏色為灰色 `--border` (`#e5e3de`)。
*   **高對比與呼吸感**：所有文字與背景的對比度必須符合 WCAG AA 級標準 (至少 4.5:1)。避免使用深色或高飽和度作為大面積卡片底色。

---

## 輸出格式

請嚴格依照以下 Markdown 格式輸出所有簡報頁面：

```markdown
# [簡報標題]
*設計系統：暖米白 Airy Glass 系統*
*Storyline：Storyline B (既有產品功能更新提案)*

---

## Slide 1: [頁面標題]
* **所選佈局模式：** Pattern X - [模式名稱]
* **視覺概念：** [簡述為什麼使用此佈局，以及如何配置空間]

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1920 1080" width="100%" height="100%">
  <defs>
    <style>
      @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@700&amp;family=Noto+Sans+TC:wght@400;700&amp;display=swap');
      .overline { font-family: 'Plus Jakarta Sans', sans-serif; font-size: 14px; font-weight: 700; fill: #007583; letter-spacing: 1.5px; text-transform: uppercase; }
      .title { font-family: 'Plus Jakarta Sans', 'Noto Sans TC', sans-serif; font-size: 48px; font-weight: 800; fill: #171c24; }
      .card-title { font-family: 'Plus Jakarta Sans', 'Noto Sans TC', sans-serif; font-size: 20px; font-weight: 700; fill: #153166; }
      .body { font-family: 'Noto Sans TC', sans-serif; font-size: 18px; font-weight: 400; fill: #171c24; line-height: 1.6; }
      .muted { font-family: 'Noto Sans TC', sans-serif; font-size: 14px; fill: #525864; }
    </style>
  </defs>

  <!-- Background -->
  <rect width="1920" height="1080" fill="#FDFCFA" />

  <!-- 內容物件繪製 -->
  
</svg>
```

### 演講講稿與備忘錄
*   **講稿口吻：** "[提供 3-5 句 PM 向主管匯報時的口吻講稿]"
*   **設計細節說明：** [說明卡片配置、Icon 及文字坐標安排]
*   **未確認事項說明：**
    *   `【To Confirm】` - [需與業務或開發團隊確認 of 假設]
    *   `【To Supplement】` - [需要使用者在簡報中填寫的真實數據欄位]

---

[依此格式重複生成剩餘的 6 頁簡報]
```

請讀取下方的 `<input_documents>` 並開始生成：

<input_documents>
### spec.md
[在這裡輸入 spec.md 的內容]

---

### plan.md
[在這裡輸入 plan.md 的內容]
</input_documents>
