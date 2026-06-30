# 0 to 1 Slide Prompt Template (全新產品提案簡報生成模板)

> **使用方式：** 
> 複製此模板的全部內容，並在最下方的 `<input_documents>` 中貼上你產品的 `spec.md` 與 `plan.md`，然後發送給 AI 助手（建議使用 Claude 3.5 Sonnet / Gemini 1.5 Pro）。它將會依照結構生成可以直接用於簡報軟體或編譯器的 SVG 簡報及演講稿。

---

## 核心任務與角色定義

你是資深產品設計師與簡報架構師。你的任務是將輸入的全新產品 `spec.md` 與 `plan.md`，轉化為一份 16:9 寬螢幕的專業產品提案簡報。每一頁簡報必須輸出為一個**完全獨立、設計精美、手工編寫的 SVG 程式碼區塊**（viewBox="0 0 1920 1080"），並附帶演講稿。

---

## 第一階段：痛點深度調研與並行搜尋 (10-Agent Fan-Out)

在開始規劃簡報前，你必須啟動**平行虛擬調研**，以補強 `spec.md` 往往缺乏的「真實世界市場數據與痛點嚴重性」：
1.  **痛點識別**：分析 `spec.md` 中產品欲解決的核心痛點（例如：人工填報耗時、錯誤率高、合規成本等）。
2.  **搜尋策略 (模擬 10 隻平行 Agent)**：自動將該痛點展開為 10 個獨立且具體的搜尋指令，去尋找國內外的權威統計數據與案例（例如：McKinsey 效率報告、Asana 工作的周邊工作指數、IDC 錯誤成本調查等）。
3.  **數據融入**：你必須在簡報的 **Slide 1 (問題探索)** 放入至少 **2 個真實的量化數據**（包含數據來源與網址連結），以此作為提案說服力的核心支柱。

---

## 第二階段：簡報 Storyline 結構 (0-to-1 全新產品專用)

全新產品簡報必須嚴格遵循以下 **6 頁結構**，模仿熟成提案的說服邏輯：

*   **Slide 1: 問題探索 (Problem Exploration)**
    *   *主標題*：產品要解決的根本性生產力損耗（大盤問題陳述）。
    *   *內容*：左側展示兩張 50/50 的真實數據大字卡 (KPI Cards)；右側展示 2 張 Pain Point Cards 剖析問題本質。
    *   *主管視角*：從主管或公司戰略出發，說明為何這是值得解決的結構性問題。
*   **Slide 2: 目標用戶與痛點 (Target Users & Pain Points)**
    *   *主標題*：起步焦慮與重複格式調整嚴重消耗目標用戶的核心心力。
    *   *內容*：明確界定目標用戶群 (Persona)，並點出他們在沒有此產品時的現有替代方案（如複製舊模板、手動編輯）及帶來的負面影響。
*   **Slide 3: 成功定義與 User Story (Success Definition & User Story)**
    *   *主標題*：成功定義：跳過空白期/痛點，在極短時間內完成核心產出。
    *   *內容*：以醒目的區塊展示標準 User Story（身為...我想要...以便...），並點出產品承諾的具體終極目標。
*   **Slide 4: 解方展現 (Solution & UI Flow)**
    *   *主標題*：主流程與介面原型設計。
    *   *內容*：左欄展示 UI 版面規劃卡片 (如精簡引導介面)；右欄展示 4 步驟的橫向流程圖，說明系統如何從輸入到產出。
*   **Slide 5: 未來指標承諾 (Future Metric Commitment)**
    *   *主標題*：我們承諾以 [北極星指標] 衡量產品價值。
    *   *內容*：大字展示產品的大盤北極星指標 (NSM) 的定義，並從主管視角說明為什麼這是一個「最誠實、最直接反映用戶價值兌現」的指標（例如以「匯出量」而非「生成量」來防範數據虛胖）。
*   **Slide 6: 驗證計畫 (Validation Plan)**
    *   *主標題*：驗證計畫：以北極星指標、量能指標與護欄指標把關成效。
    *   *內容*：**2 層階層式指標樹 (Hierarchical Tree)**。
        *   第一層：產品北極星指標 (NSM) ＋ 採用理由。
        *   第二層：量能指標 (Volume) ＋ 採用理由 (左) ｜ 護欄指標 (Guardrail) (設定中位數 ≦ 5 次，如對話輪數) ＋ 採用理由 (右)。
        *   *制約*：**全新產品提案嚴禁出現功能層成功指標 (FSM)**，以免造成觀念誤導。
    *   *主管視角*：說明以匯出量防範試用虛胖、以對話輪數把關品質的設計 rationale。

---

## 第三階段：資料視覺化與佈局規範 (72 Layout Selector)

每一頁簡報必須挑選適合的佈局結構，嚴格禁止文字直接鋪滿或擁擠排版。參考以下資料視覺化佈局：
*   **數據大字卡 (Pattern #40)**：用於 Slide 1 或 Slide 5。使用 60px-64px 的大數字，下方搭配 14px-15px 的單位與來源說明。
*   **對稱左右拆分卡片 (Pattern #48)**：用於 Slide 2 或 Slide 3。左右對等拆分，給予充足的 24px-30px 邊距與間距，保證呼吸感。
*   **橫向步驟流程鏈 (Pattern #39)**：用於 Slide 4。使用白色背景的卡片框線，搭配中間的引導箭頭或連線。
*   **層級指標樹 (Pattern #44)**：用於 Slide 6。使用 SVG 直線/折線連接各指標節點，結構清晰。

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
*Storyline：Storyline A (全新產品提案)*

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

[依此格式重複生成剩餘的 5 頁簡報]
```

請讀取下方的 `<input_documents>` 並開始生成：

<input_documents>
### spec.md
[在這裡輸入 spec.md 的內容]

---

### plan.md
[在這裡輸入 plan.md 的內容]
</input_documents>
