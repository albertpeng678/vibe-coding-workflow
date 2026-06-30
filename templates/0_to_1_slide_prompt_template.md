# 0 to 1 Slide Prompt Template (全新產品提案 Gamma Prompt 生成模板)

> **使用方式：** 
> 複製此模板的全部內容，並在最下方的 `<input_documents>` 中貼上你產品的 `spec.md` 與 `plan.md`，然後發送給 AI 助手。它將會產出一份**可以直接複製貼進 Gamma 簡報生成軟體的 Prompt（含大綱與嚴格風格指令）**，以及每一頁的演講講稿。

---

## 核心任務與角色定義

你是資深產品經理與簡報規劃專家。你的任務是將輸入的全新產品 `spec.md` 與 `plan.md`，轉化為一份**給 AI 簡報生成軟體（如 Gamma）使用的優化 Prompt**。這份 Prompt 必須包含「結構化的簡報大綱（Markdown 格式）」以及「嚴格的視覺風格與排版指令」，以確保 Gamma 能夠完美生成高呼吸感、結構清晰的簡報。

---

## 第一階段：痛點深度調研與並行搜尋 (10-Agent Fan-Out)

在開始規劃大綱前，你必須啟動**平行虛擬調研**，以補強 `spec.md` 往往缺乏的「真實世界市場數據與痛點嚴重性」：
1.  **痛點識別**：分析 `spec.md` 中產品欲解決的核心痛點（例如：人工填報耗時、錯誤率高、合規成本等）。
2.  **搜尋策略 (模擬 10 隻平行 Agent)**：自動將該痛點展開為 10 個獨立且具體的搜尋指令，去尋找國內外的權威統計數據與案例（例如：McKinsey 效率報告、Asana 工作的周邊工作指數、IDC 錯誤成本調查等）。
3.  **數據融入**：你必須在簡報的 **Slide 1 (問題探索)** 放入至少 **2 個真實的量化數據**（包含數據來源與網址連結），以增強提案的說服力。

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

## Slide 2: [第二頁標題]
*   目標用戶：[Persona]
*   現有替代方案與痛點：[說明]

## Slide 3: [第三頁標題]
*   User Story：身為...我想要...以便...
*   核心承諾與成功狀態：[說明]

## Slide 4: [第四頁標題]
*   產品解方與 Wizard 介面規劃：[說明]
*   運作流程：步驟 1 -> 步驟 2 -> 步驟 3 -> 步驟 4

## Slide 5: [第五頁標題]
*   大盤北極星指標 (NSM)：[定義]
*   指標採用理由：[說明]

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

### 演講講稿與備忘錄

#### Slide 1: [第一頁標題]
*   **講稿口吻：** "[提供 3-5 句 PM 向主管匯報時的口吻講稿]"
*   **未確認事項：** `【To Confirm】` [說明] ｜ `【To Supplement】` [說明]

#### Slide 2: [第二頁標題]
*   **講稿口吻：** "[講稿]"
*   **未確認事項：** [說明]

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
