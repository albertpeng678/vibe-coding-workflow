# 0 to 1 Slide Prompt Template (全新產品提案 Gamma Prompt 生成模板)

> **使用方式：** 
> 複製此模板的全部內容，並在最下方的 `<input_documents>` 中貼上你產品的 `spec.md` 與 `plan.md`，然後發送給 AI 助手。它將會產出一份**可以直接複製貼進 Gamma 簡報生成軟體的 Prompt（含大綱與嚴格風格指令）**，以及每一頁的演講講稿。

---

## 核心任務與角色定義

你是資深產品經理與簡報規劃專家。你的任務是將輸入的全新產品 `spec.md` 與 `plan.md`，轉化為一份**給 AI 簡報生成軟體（如 Gamma）使用的優化 Prompt**。這份 Prompt 必須包含「結構化的簡報大綱（Markdown 格式）」以及「嚴格的視覺風格與排版指令」，以確保 Gamma 能夠完美生成高呼吸感、結構清晰的簡報。

---

## 🤖 智能體設計模式執行指南 (Agentic Design Patterns Execution)

為了確保產出簡報的高品質與指標的絕對嚴謹性，你（執行此 Prompt 的 LLM）必須依照以下 **提示鏈、多角色稽核與反思規劃 (Chaining, Multi-Agent Audit & Reflection Patterns)** 順序執行：

### 1. 執行路義規劃 (Planning & Chaining Phase)
*   **第一步（分析輸入）**：解析 `<input_documents>`，提取核心產品願景與欲解決的痛點。
*   **第二步（並行搜尋調研 - Fan-out）**：針對痛點自動展開 10 個搜尋查詢，模擬 10 隻子 Agent 並行調研真實世界數據與網址。
*   **第三步（草擬簡報大綱）**：依照「問題優先」的故事線與「資料視覺化」佈局規則，草擬 6 頁簡報大綱。
*   **第四步（雙重嚴苛稽核官審查 - Multi-Agent Audit）**：對每一頁簡報與指標，執行下方的「雙重稽核官關卡」與指標規則。
*   **第五步（最終輸出）**：只有在每一頁簡報同時通過雙重稽核官的 **各三個綠燈 (🟢🟢🟢) 共六個綠燈** 審查後，方可輸出最終的 Gamma Prompt。

### 2. 雙重稽核官關卡 (Double-Auditor Gatekeeper)
你必須虛擬分身為兩位最嚴苛的審查官，逐頁進行對抗性稽核。若未通過，必須指出缺陷 (Gap)、修改內容、並重新進行稽核直至過關：

#### 👤 指標稽核官 (Metrics Audit Officer)
*   **指標稽核三綠燈標準 (🟢🟢🟢)**：
    1.  `🟢` **價值度量**：北極星指標 (NSM) 必須衡量「使用者感受到的價值」(需求面)，嚴禁採用「系統做了什麼」的供給面指標，且該指標必須在當前條件下可量測。
    2.  `🟢` **0-1 結構合規**：**全新產品提案 (0 to 1) 嚴禁出現功能層成功指標 (FSM)**。驗證計畫僅限兩層結構 (NSM ➔ Volume / Guardrail)。若出現任何功能層指標，立即亮紅燈。
    3.  `🟢` **防衛健康**：量能指標必須為全域加總（防範 session 偏差）；護欄指標必須是可量測的比率 (0-100%)，嚴禁採用「= 0」這種無法迭代的絕對值或已被工程解決的偽指標。

#### 👤 PM 總監稽核官 (PM Director Audit Officer)
*   **故事線稽核三綠燈標準 (🟢🟢🟢)**：
    1.  `🟢` **故事線通順度**：6 頁故事線必須完美契合「問題優先」的主線（問題 ➔ Persona ➔ 成功定義 ➔ 解方 ➔ 運作與 NSM ➔ 驗證計畫），前後因果邏輯必須緊密相扣，轉換流暢自然。
    2.  `🟢` **主管視角 (Executive Rationale)**：投影片標題必須是白話結論，非內部術語 (如 STEP X)。簡報內容必須具備宏觀商業視角，向高管說清楚為何該痛點非解不可、為何此指標是核心價值的誠實代表。
    3.  `🟢` **術語過濾與定義**：簡報中出現的所有專有名詞（如北極星、護欄等），必須在第一次出現的頁面中進行白話文定義後才能使用。

---

## 📊 指標定義與 Few-Shot 指引 (Metrics Blueprint & Few-Shots)

指標稽核官必須嚴格使用以下定義與 Few-Shot 範例來檢查驗證計畫中的指標，避免自嗨與無效指標：

### 1. 北極星指標 (North Star Metric - NSM)
*   **定義**：度量產品核心價值向用戶兌現的單一領先指標。必須站在**需求面（用戶感受到的價值）**，代表用戶「真的把產出用在實際工作流中」，而非「系統單方面產出了東西」（供給面），也非落後的營收指標。
*   **如何理解「用戶感受到的價值」**：用戶在系統點擊「生成」不代表感受到價值（可能是廢稿）；唯有使用者「匯出檔案」、「複製內容」或「分享給協作者」時，才代表價值真正兌現。
*   **Few-Shot 範例**：
    *   ❌ *供給面/自嗨*：每週 AI 生成 PRD 的總次數（用戶可能生成後立即刪除，未感受到價值）。
    *   ✅ *用戶感受價值*：每週成功 **匯出或分享** 的 AI PRD 總數量（匯出代表內容已通過人工檢視且將進入下一步工作流）。
    *   ❌ *落後/財務*：付費訂閱用戶數（無法指導產品改進的結果指標）。
    *   ✅ *用戶感受價值*：每週有進行內容分享或協作的活躍 workspace 數量。

### 2. 功能層成功指標 (Feature Success Metric - FSM)
*   **定義**：用以量測該特定新增功能模組的採用與轉化率。**注意：在 0-to-1 全新產品提案中，此指標嚴禁出現 (FSM = 0)**，因為全新產品沒有大盤與子功能的區分，引入 FSM 會造成高管觀念混淆。

### 3. 量能指標 (Volume Metric)
*   **定義**：度量漏斗最前端的曝光與觸發次數，用以反映產品的採用規模。必須是**全域加總**（如每週總次數），以避免平均數（如每 Session 平均次數）被少數重度用戶或異常長 Session 灌歪。
*   **Few-Shot 範例**：
    *   ❌ *易灌歪平均數*：每 Session 使用者平均提問次數。
    *   ✅ *全域加總*：每週總上傳分析的 PDF 文件數量。

### 4. 護欄指標 (Guardrail Metric)
*   **定義**：量測品質、安全性、用戶疲勞度或系統副作用的指標。必須是**可優化的比率 (0-100%)**，不能使用「= 0」這種無法迭代的絕對限制，亦不能使用高變異難以監測的量（如平均對話時長），且必須避開已被技術解決的偽問題。
*   **Few-Shot 範例**：
    *   ❌ *絕對值門檻*：API 錯誤次數 = 0（無法衡量過程表現，無法進行灰度優化）。
    *   ✅ *可優化比率*：每週 AI 產出內容的**人工作業修正率**（如修改輪數超過 5 次的比例 ≦ 10%）。
    *   ❌ *偽問題*：系統未斷線率（若基礎建設已保證 99.9% 穩定，此指標無業務優化空間）。
    *   ✅ *品質護欄*：Verifier Agent 判定引用文獻 (Citations) 為 verified 的比例 ≧ 95%（直接為財務級審計把關品質）。

---

## 第一階段：痛點深度調研與並行搜尋 (10-Agent Fan-Out)

1.  **痛點識別**：分析 `spec.md` 中產品欲解決的核心痛點（例如：人工填報耗時、錯誤率高、合規成本等）。
2.  **搜尋策略 (模擬 10 隻平行 Agent)**：自動將該痛點展開為 10 個獨立且具體的搜尋指令，去尋找國內外的權威統計數據與案例。
3.  **數據融入**：你必須在簡報的 **Slide 1 (問題探索)** 放入至少 **2 個真實的量化數據**（包含數據來源與網址連結），以此作為提案說服力的核心支柱。

---

## 第二階段：簡報 Storyline 結構 (0-to-1 全新產品專用)

全新產品簡報大綱必須嚴格遵循以下 **6 頁結構**，模仿熟成提案的說服邏輯：

*   **Slide 1: 問題探索 (Problem Exploration)**
    *   *大標題*：產品要解決的根本性生產力損耗（大盤問題陳述）。
    *   *內容*：包含 2 組真實的外部數據（含來源）；條列問題本質與非解不可的代價。
*   **Slide 2: 目標用戶與痛點 (Target Users & Pain Points)**
    *   *大標題*：起步焦慮與重複格式調整嚴重消耗目標用戶的核心心力。
    *   *內容*：界定目標用戶 Persona，列出其現有替代方案（如複製舊模板）與 2 大核心痛點。
*   **Slide 3: 成功定義與 User Story (Success Definition & User Story)**
    *   *大標題*：成功定義：跳過空白期/痛點，在極短時間內完成核心產出。
    *   *內容*：標準 User Story（身為...我想要...以便...）以及產品所承諾的具體指標。
*   **Slide 4: 解方展現 (Solution & UI Flow)**
    *   *大標題*：主流程與介面原型設計。
    *   *內容*：說明 Wizard 嚮導介面規劃與系統處理流程。
*   **Slide 5: 未來指標承諾 (Future Metric Commitment)**
    *   *大標題*：我們承諾以 [北極星指標] 衡量產品價值。
    *   *內容*：定義大盤北極星指標 (NSM)（例如週匯出量），並說明為什麼採用此指標做為價值代理指標。
*   **Slide 6: 驗證計畫 (Validation Plan)**
    *   *大標題*：驗證計畫：以北極星指標、量能指標與護欄指標把關成效。
    *   *內容*：
        *   第一層：產品北極星指標 (NSM) ＋ 採用理由。
        *   第二層：量能指標 (Volume) ＋ 採用理由 ｜ 護欄指標 (Guardrail，設定中位數 ≦ 5 次，如對話輪數) ＋ 採用理由。
        *   *制約*：**全新產品提案嚴禁出現功能層成功指標 (FSM)**，以免造成觀念誤導。

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
# [產品提案簡報標題] - Gamma AI 適用 Prompt 與大綱

複製以下 `--- START OF GAMMA PROMPT ---` 與 `--- END OF GAMMA PROMPT ---` 之間的所有內容，貼入 Gamma 的 AI 導入視窗中生成簡報：

```text
--- START OF GAMMA PROMPT ---

Create a 16:9 widescreen presentation using a minimalist, high-contrast style with a warm paper white background (#FDFCFA) and deep navy blue accents (#153166). Follow the outline below:

# [簡報標題]

## Slide 1: [第一頁標題]
*   [數據 1] (來源/網址)
*   [數據 2] (來源/網址)
*   問題本質：[說明]
*   非解不可的代價：[說明]

...

## Slide 6: [第六頁標題]
*   驗證指標樹 (無功能層指標)：
    *   北極星指標 (NSM)：[定義] ➔ 理由：[說明]
    *   量能指標 (Volume)：[定義] ➔ 理由：[說明]
    *   護欄指標 (Guardrail) ≦ 5 次 (依 query_round 統計)：[定義] ➔ 理由：[說明]

### 🎨 Design & Style Directives for Gamma:
- **Theme**: Minimalist visual style, large typography, high contrast, airy layout with generous padding and margins (breathing room).
- **Colors**: Background #FDFCFA, Primary Accent #153166, Brand Highlight #48B7BD, Body Text #171C24, Alerts #B91C1C.
- **Constraints**: Strictly forbid all emojis. Keep text density low (Brief). Max 3 items per card.
- **Layouts**: Use large metrics callouts for Slide 1, 2-column split cards for Slide 2 & 3, horizontal step list for Slide 4, and a hierarchical connection list for Slide 6.

--- END OF GAMMA PROMPT ---
```

### 雙重稽核關卡報告 (Audit Reports)

| 頁碼 | 頁面主題/大標題 | 指標稽核官評審 | PM 總監稽核官評審 | 狀態 |
| :--- | :--- | :--- | :--- | :--- |
| Slide 1 | [標題] | 🟢🟢🟢 (通過理由) | 🟢🟢🟢 (通過理由) | 🟢 PASS |
| Slide 2 | [標題] | 🟢🟢🟢 (通過理由) | 🟢🟢🟢 (通過理由) | 🟢 PASS |
| Slide 3 | [標題] | 🟢🟢🟢 (通過理由) | 🟢🟢🟢 (通過理由) | 🟢 PASS |
| Slide 4 | [標題] | 🟢🟢🟢 (通過理由) | 🟢🟢🟢 (通過理由) | 🟢 PASS |
| Slide 5 | [標題] | 🟢🟢🟢 (通過理由) | 🟢🟢🟢 (通過理由) | 🟢 PASS |
| Slide 6 | [標題] | 🟢🟢🟢 (已驗證無FSM) | 🟢🟢🟢 (已驗證故事連貫) | 🟢 PASS |

> *註：若有任何頁面初測亮紅燈 (🔴)，請在此處列出 `【修正紀錄】` 與修改前後對比。*

### 演講講稿與備忘錄

#### Slide 1: [第一頁標題]
*   **講稿口吻：** "[提供 3-5 句 PM 向主管匯報時的口吻講稿]"
*   **未確認事項：** `【To Confirm】` [說明] ｜ `【To Supplement】` [說明]

[重複輸出至 Slide 6]
```

請讀取下方的 `<input_documents>` 並開始生成：

<input_documents>
### spec.md
[在這裡輸入 spec.md 的內容]

---

### plan.md
[在這裡輸入 plan.md 的內容]
</input_documents>
