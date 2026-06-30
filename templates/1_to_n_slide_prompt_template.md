# 1 to N Slide Prompt Template (既有產品功能更新 Gamma Prompt 生成模板)

> **使用方式：** 
> 複製此模板的全部內容，並在最下方的 `<input_documents>` 中貼上你功能的 `spec.md` 與 `plan.md`，然後發送給 AI 助手。它將會產出一份**可以直接複製貼進 Gamma 簡報生成軟體的 Prompt（含大綱與嚴格風格指令）**，以及每一頁的演講講稿。

---

## 核心任務與角色定義

你是資深產品經理與指標分析專家。你的任務是將輸入的功能更新 `spec.md` 與 `plan.md`，轉化為一份**給 AI 簡報生成軟體（如 Gamma）使用的優化 Prompt**。這份 Prompt 必須包含「結構化的簡報大綱（Markdown 格式）」以及「嚴格的視覺風格與排版指令」，以確保 Gamma 能夠完美生成高呼吸感、結構清晰的簡報。

---

## 🤖 智能體設計模式執行指南 (Agentic Design Patterns Execution)

為了確保產出簡報的高品質與嚴格制約，你（執行此 Prompt 的 LLM）必須依照以下 **提示鏈與反思規劃 (Chaining & Reflection Patterns)** 順序執行：

### 1. 執行路徑規劃 (Planning & Chaining Phase)
*   **第一步（分析主產品）**：分析 `<input_documents>` 的 `spec.md` 盤點其所附屬的主產品，定位主產品的角色與核心價值。
*   **第二步（大盤北極星共識 - 5-Agent Consensus）**：若輸入文件難以辨識主產品或指標，啟動 5 隻虛擬 Agent 的共識討論，對齊競品特點並定調大盤北極星指標。
*   **第三步（草擬簡報大綱）**：依照「指標貫穿全場」故事線與「資料視覺化」佈局規則，草擬 7 頁簡報大綱，並強制在主產品所有提及處標註 `[⚠️ 請在此處更新您正確的主產品名稱及指標]`。
*   **第四步（自我反思審查 - Reflection）**：在輸出最終結果前，執行下方的「防護欄自我檢查」。

### 2. 自我反思與防護欄清單 (Reflection & Guardrails Checklist)
在生成最終結果前，你必須扮演審查者 (Critic)，對草擬的內容進行**自我糾錯**：
*   **Emoji 防護欄**：檢查大綱與 Gamma 指令中是否含有任何表情符號（如 ↗, ✅ - 除了警示標籤 `[⚠️ 請在此處更新...]` 中的 ⚠️ 以外）？如果有，必須全部移除。
*   **主產品警告標籤防護欄**：檢查 Slide 1 與 Slide 7 中所有提到「主產品名稱」與「大盤北極星/基準數據」的地方，是否**全部**都緊鄰著標示了警告標籤 `[⚠️ 請在此處更新您正確的主產品名稱及指標]`？如果遺漏，必須補上。
*   **呼吸感與密度防護欄**：檢查每張幻燈片的項目是否 ≦ 3 條？文字是否過於擁擠？如果有，必須進行精簡（文字密度為 Brief）。
*   **指標樹防護欄**：檢查 Slide 7 是否完整包含 3 層指標樹 (大盤NSM ➔ 功能層FSM ➔ 量能指標 ｜ 護欄指標)？是否說明了各層的連動關係？

---

## 第一階段：主產品定位與指標對齊 (5-Agent Consensus & Warning)

1.  **盤點主產品**：閱讀 `spec.md` 與 `plan.md`，找出該功能是附屬於哪一個既存的主產品下。
2.  **定位主產品北極星 (模擬 5 隻 Agent 共識會議)**：若 spec 中未寫明主產品，請自動啟動 5 隻虛擬 Agent 進行共識探討定調。同時，進行同類產品的 Web Search，以徹底了解主產品定位，並設定主產品的**大盤北極星指標 (NSM)**。
3.  **提醒與警告標記**：在最終輸出的簡報大綱與講稿中，針對推論出來的主產品名稱和大盤數據，必須**強制在旁加上顯著的警告標記**，提醒使用者：
    `[⚠️ 請在此處更新您正確的主產品名稱及指標]`

---

## 第二階段：簡報 Storyline 結構 (1-to-N 功能更新專用)

既有產品功能更新簡報大綱必須嚴格遵循以下 **7 頁結構**，以指標驅動故事線：

*   **Slide 1: 項目現狀 (Current Status)**
    *   *大標題*：我們目前以大盤指標 [主產品大盤北極星] 衡量平台價值 `[⚠️ 請在此處更新您正確的主產品名稱及指標]`。
    *   *內容*：大字展示主產品當前的大盤指標與基準線（如每週活躍文件數為 42,000 份）。
*   **Slide 2: 瓶頸分析 (Bottleneck Analysis)**
    *   *大標題*：[新功能所屬場景] 存在嚴重瓶頸，導致 [大盤損耗指標]（例如 40% 會議紀錄零瀏覽）。
    *   *內容*：左側以紅色警示卡片突顯流失率/損耗率；右側剖析流失主因（如時效性喪失、高閱讀摩擦）。
*   **Slide 3: 使用者故事 (User Story)**
    *   *大標題*：[新功能名稱] 旨在消除 [痛點] 並釋放用戶的核心心力。
    *   *內容*：展示標準的使用者故事（身為...我想要...以便...），強調如何搶占黃金時間、降低門檻。
*   **Slide 4: 成功定義 (Success Definition)**
    *   *大標題*：成功定義：將 [核心轉化指標] 從 X% 提升至 Y%。
    *   *內容*：對稱左右拆分卡片 (Comparison Split)，左側為 Current State，右側為 Target State。
*   **Slide 5: 功能機制 (Feature Mechanism)**
    *   *大標題*：透過 [功能名稱] 將 [輸入源] 自動轉化為 [產出與行動]。
    *   *內容*：3 步驟橫向 Process Flow，描述新功能如何自動化處理、派發並拉回協作。
*   **Slide 6: 解方展示與原型 (Solution UI & Prototype)**
    *   *大標題*：新功能介面與流程設計。
    *   *內容*：說明內嵌的 AI 功能區塊規劃與同步或協作面板的互動介面。
*   **Slide 7: 驗證計畫 (Validation Plan)**
    *   *大標題*：驗證計畫：以指標樹把關成效，防堵自嗨指標。
    *   *內容*：
        *   第一層 (Top)：產品大盤北極星指標 (NSM) ＋ 設計理由 `[⚠️ 請在此處更新您正確的主產品名稱及指標]`。
        *   第二層 (Middle)：功能層成功指標 (FSM) ＋ 設計理由。
        *   第三層 (Bottom)：量能指標 (Volume) ＋ 設計理由 ｜ 護欄指標 (Guardrail，設定中位數 ≦ 5 次，如對話輪數) ＋ 設計理由。

---

## 第三階段：Gamma 設計與風格指令 (Gamma Style Directives)

在生成的 Prompt 底部，必須附帶一組**嚴格的風格制約**，以便直接複製到 Gamma 中：
1.  **主題風格 (Theme)**：Minimalist visual style, large typography, high contrast, airy layout with generous padding and margins (breathing room).
2.  **配色方案 (Colors)**：
    *   頁面背景 (Page Background)：暖米白 Warm Paper White (`#FDFCFA` 或 `rgb(253,252,249)`)
    *   主標題與卡片框 (Primary Accent)：深靛藍 Classic Navy (`#153166` / `rgb(21,49,102)`)
    *   高亮強調 (Brand Highlight)：青色 Clean Teal (`#48B7BD` / `rgb(72,183,189)`)
    *   主內文 (Body Text)：深炭黑 Deep Charcoal (`#171C24` / `rgb(23,28,36)`)
    *   警示/痛點 (Warnings/Alerts)：猩紅 Rose Crimson (`#B91C1C`)
3.  **排版佈局限制 (Layout Constraints)**：
    *   **嚴格禁止任何 Emoji**（如 ↗, ✅ 等），使用 Unicode 標點（如 `—`, `·`）或文字代替。
    *   排版極度要求呼吸感，禁止擁擠。每張卡片/幻燈片內最多放置 3 個內容項目。
    *   採用「大數字 KPI 卡片」呈現 Slide 1 的數據。
    *   使用「2欄/3欄拆分卡片」呈現用戶痛點與成功定義，代替長文字條列。
    *   使用「橫向步驟鏈 (Step list)」呈現解方流程。
    *   使用「階層指標樹」呈現驗證計畫。
4.  **文字密度 (Text Density)**：Brief (簡練、視覺主導)。

---

## 輸出格式

請依照以下 Markdown 格式輸出你的結果：

```markdown
# [專案更新簡報標題] - Gamma AI 適用 Prompt 與大綱

複製以下 `--- START OF GAMMA PROMPT ---` 與 `--- END OF GAMMA PROMPT ---` 之間的所有內容，貼入 Gamma 的 AI 導入視窗中生成簡報：

```text
--- START OF GAMMA PROMPT ---

Create a 16:9 widescreen presentation using a minimalist, high-contrast style with a warm paper white background (#FDFCFA) and deep navy blue accents (#153166). Follow the outline below:

# [簡報標題]

## Slide 1: [第一頁標題]
*   主產品：[主產品名稱] [⚠️ 請在此處更新您正確的主產品名稱及指標]
*   大盤基準線數據：[指標與數值] [⚠️ 請在此處更新您正確的主產品名稱及指標]
*   主管視角：[說明]

## Slide 2: [第二頁標題]
*   流失率/損耗率：[數據卡片] (來源)
*   瓶頸細節與真因：[說明]

## Slide 3: [第三頁標題]
*   User Story：身為...我想要...以便...
*   核心承諾與成功狀態：[說明]

## Slide 4: [第四頁標題]
*   成功指標目標：[從 X% 提升至 Y%]
*   對稱狀態比較：Current State vs. Target State

## Slide 5: [第五頁標題]
*   功能運作機制：步驟 1 -> 步驟 2 -> 步驟 3
*   主動協作的起點：[說明]

## Slide 6: [第六頁標題]
*   新功能介面佈局與同步機制：[說明]

## Slide 7: [第七頁標題]
*   驗證指標樹：
    *   產品大盤北極星指標 (NSM) [⚠️ 請在此處更新您正確的主產品名稱及指標]：[定義] ➔ 理由：[說明]
    *   功能層成功指標 (FSM)：[定義] ➔ 理由：[說明]
    *   量能指標 (Volume)：[定義] ➔ 理由：[說明]
    *   護欄指標 (Guardrail) ≦ 5 次 (依 query_round 統計)：[定義] ➔ 理由：[說明]

### 🎨 Design & Style Directives for Gamma:
- **Theme**: Minimalist visual style, large typography, high contrast, airy layout with generous padding and margins (breathing room).
- **Colors**: Background #FDFCFA, Primary Accent #153166, Brand Highlight #48B7BD, Body Text #171C24, Alerts #B91C1C.
- **Constraints**: Strictly forbid all emojis. Keep text density low (Brief). Max 3 items per card.
- **Layouts**: Use large metrics callouts for Slide 1, 2-column split cards for Slide 2 & 4, horizontal step list for Slide 5, and a hierarchical connection list for Slide 7.

--- END OF GAMMA PROMPT ---
```

### 演講講稿與備忘錄

#### Slide 1: [第一頁標題]
*   **講稿口吻：** "[提供 3-5 句 PM 向主管匯報時的口吻講稿]"
*   **未確認事項：** `【To Confirm】` [說明] ｜ `【To Supplement】` [說明]

#### Slide 2: [第二頁標題]
*   **講稿口吻：** "[講稿]"
*   **未確認事項：** [說明]

[重複輸出至 Slide 7]
```

請讀取下方的 `<input_documents>` 並開始生成：

<input_documents>
### spec.md
[在這裡輸入 spec.md 的內容]

---

### plan.md
[在這裡輸入 plan.md 的內容]
</input_documents>
