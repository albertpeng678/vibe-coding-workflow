# Slide Prompt Template Optimization Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rebuild the "澄清機制／雙重稽核官／標題頁／流程圖策略／風格指令" of the two Gamma slide-prompt templates (`1_to_n_slide_prompt_template.md`, `0_to_1_slide_prompt_template.md`) per the approved design, and extract the shared logic into a new `templates/_shared-modules.md` source-of-truth file.

**Architecture:** These are prompt-engineering markdown documents, not executable code — there is no test runner. "Tests" in this plan are deterministic `grep`/`Read` verification steps: confirm new required strings exist, confirm superseded strings are gone, confirm the shared module and both templates stay textually in sync at each `<!-- SYNC: ... -->` anchor. Each task edits one conceptual module across all three files it touches (the shared module + both templates) so a reviewer can gate on "does this module read correctly and consistently everywhere."

**Tech Stack:** Markdown only. No build step, no package manager, no test framework.

## Global Constraints

- Both templates must remain **fully self-contained, copy-paste-able single files** — nothing may be turned into a live file reference/include; `_shared-modules.md` is a maintainer-facing source of truth only, synced by hand via `<!-- SYNC: _shared-modules.md#<anchor> -->` comments placed directly above each synced block in both templates.
- No emoji anywhere in generated template instructions (existing project convention — Lucide icons only where the project already uses `{{icon:name}}`-style markers; these two templates use plain text/checkbox markers, keep that).
- Brand colors (verbatim, do not alter): background `#FDFCFA`, Primary Navy `#153166`, Brand Strong Teal `#007583` (replaces the old `#48B7BD`), Secondary Text Slate `#525864` (new), Alert Rose Crimson `#B91C1C`.
- Forbidden in any text that could end up inside the **generated presentation content** (Slide titles/body/speaker notes): `自嗨`, `虛胖`, `腦補`, `洗版`, `灌水` — these words may only appear inside the templates' own internal instructional text (e.g., inside the Few-Shot "❌ bad example" labels and inside the new Output Register Guardrail rule that names them as forbidden).
- The 1-to-N template's 3-tier metric tree keeps FSM (功能層成功指標); the 0-to-1 template forbids FSM entirely — do not blur this distinction when editing the shared metrics module.
- Every edit must preserve each file's existing heading hierarchy and numbering style (`## 第N階段：...`, `### N. ...`) so the rest of the unedited document still reads coherently.

---

## File Structure

| File | Status | Responsibility |
|---|---|---|
| `templates/_shared-modules.md` | **New** | Maintainer-facing single source of truth for the 6 shared modules (metrics, confidence-tiered clarification, double-auditor rules incl. output register guardrail, cover-slide formula, simplified Gamma style directives, Mermaid diagram strategy). Not referenced at runtime by either template — copy-paste source only. |
| `templates/1_to_n_slide_prompt_template.md` | Modified | 1-to-N (existing-product feature update) Gamma prompt generator, 7-slide storyline. |
| `templates/0_to_1_slide_prompt_template.md` | Modified | 0-to-1 (new-product proposal) Gamma prompt generator, 6-slide storyline. |

---

## Task 1: Scaffold `_shared-modules.md` and migrate the metrics module

**Files:**
- Create: `templates/_shared-modules.md`
- Modify: `templates/1_to_n_slide_prompt_template.md` (§"📊 指標定義與 Few-Shot 指引", currently lines 42-93)
- Modify: `templates/0_to_1_slide_prompt_template.md` (§"📊 指標定義與 Few-Shot 指引", currently lines 42-84)

**Interfaces:**
- Produces: `_shared-modules.md` file with a top-level TOC linking anchors `#module-1-指標定義與-few-shot`, `#module-2-信心分級澄清機制`, `#module-3-雙重稽核官規則`, `#module-4-標題頁公式`, `#module-5-gamma-風格精簡指令`, `#module-6-mermaid-流程圖策略` (the remaining 5 anchors are stubbed with a one-line "（Task N 補上）" placeholder that later tasks fill in — this is the one allowed exception to "no placeholders" because it is a scaffold marker for a doc that will be completed within this same plan, not a shipped deliverable).
- Consumes: nothing (first task).

### Steps

- [ ] **Step 1: Create `templates/_shared-modules.md` with the file skeleton**

```markdown
# 共用模組（Shared Modules）— 兩份 Slide Prompt Template 的維護端單一真實來源

> **這份檔案不是給使用者複製貼上用的。** 它是 `1_to_n_slide_prompt_template.md` 與
> `0_to_1_slide_prompt_template.md` 的共用邏輯維護來源。修改共用邏輯時，先改這裡，
> 再手動同步貼回兩份 template 中標記了 `<!-- SYNC: _shared-modules.md#<anchor> -->`
> 的對應區塊。

## 目錄

1. [指標定義與 Few-Shot](#module-1-指標定義與-few-shot)
2. [信心分級澄清機制](#module-2-信心分級澄清機制)
3. [雙重稽核官規則](#module-3-雙重稽核官規則)
4. [標題頁公式](#module-4-標題頁公式)
5. [Gamma 風格精簡指令](#module-5-gamma-風格精簡指令)
6. [Mermaid 流程圖策略](#module-6-mermaid-流程圖策略)

---

## Module 1: 指標定義與 Few-Shot

（本節內容於本任務填入）

---

## Module 2: 信心分級澄清機制

（Task 2 補上）

---

## Module 3: 雙重稽核官規則

（Task 3 補上）

---

## Module 4: 標題頁公式

（Task 4 補上）

---

## Module 5: Gamma 風格精簡指令

（Task 5 補上）

---

## Module 6: Mermaid 流程圖策略

（Task 6 補上）
```

- [ ] **Step 2: Fill in Module 1 content in `_shared-modules.md`**

Replace the `（本節內容於本任務填入）` line under `## Module 1: 指標定義與 Few-Shot` with:

```markdown
> **適用範圍**：北極星指標 (NSM)、量能指標 (Volume)、護欄指標 (Guardrail) 三者的定義與
> Few-Shot 對**兩份 template 完全共用**。功能層成功指標 (FSM) **僅 1-to-N 適用**，
> **0-to-1 嚴禁出現** —— 兩份 template 在下方各自的「1-to-N 結構合規」／「0-1 結構合規」
> 稽核準則裡各自保留這條差異規則，不要因為共用了指標定義就把 FSM 也共用進 0-to-1。

### 1. 北極星指標 (North Star Metric - NSM)

*   **定義**：度量產品核心價值向用戶兌現的單一領先指標。必須站在**需求面（用戶感受到的價值）**，代表用戶「真的體驗到價值」的最直接、最誠實的代理行為。
*   **廚房比喻**：**「每週吃光光盤的總數量」**（吃光代表顧客覺得東西好吃、體驗到食物價值的誠實身體行為；統計上只需數盤子，統計摩擦極低）。
*   **設計與稽核原則**：
    *   **價值實現代理**：用戶在系統點擊「生成」不代表感受到價值；必須是「匯出檔案」、「複製內容」或「分享給協作者」等代表內容已被人工檢視且即將進入下一步工作流的動作。
    *   **避開百分比陷阱**：北極星指標一律使用**「絕對計數」**（例如：每週成功匯出的 PRD 數量），以衡量業務規模與實質用戶價值的總和。避免使用率或百分比。
    *   **硬性採用理由**：在簡報中必須詳細說明為什麼該指標代表核心價值的兌現，並解釋為什麼排除註冊數或營收等未能反映使用者實際感受價值的供給面/落後指標。
*   **Few-Shot 範例**：
    *   ❌ *供給面/未反映使用者價值*：每週 AI 生成 PRD 的總次數（用戶可能生成後立即刪除，未感受到價值）。
    *   ✅ *用戶感受價值*：每週成功 **匯出或分享** 的 AI PRD 總數量（匯出代表內容已通過人工檢視且將進入下一步工作流）。
    *   ❌ *落後/財務*：付費訂閱用戶數（無法指導產品改進的結果指標）。
    *   ✅ *用戶感受價值*：每週有進行內容分享或協作的活躍 workspace 數量。

### 2. 功能層成功指標 (Feature Success Metric - FSM) —— 僅 1-to-N 適用

*   **定義**：用以量測該特定新增功能模組的採用與核心價值轉化。它必須同時包含**「採用該功能」**與**「體驗到主產品核心價值」**兩個要件，用以證明該功能如何發揮觸媒作用，拉動主產品的北極星指標。
*   **廚房比喻**：**「點了『AI 主廚推薦新菜』且吃光的顧客人數」**（同時滿足「點了新菜（採用功能）」且「吃光（核心價值實現）」）。
*   **設計與稽核原則**：
    *   **指標拉動理由**：必須說明此指標如何作為優化槓桿拉動主產品的北極星指標 (NSM)。
    *   **避開高摩擦動作**：在實務中，要求團隊成員對摘要進行留言或勾選的門檻極高。因此，改採「除建立者外的團隊瀏覽」作為低摩擦但有效的協作與對齊代理行為。
*   **Few-Shot 範例**（主產品：Notion 平台，其 NSM = 每週活躍協作文件數；新增功能：AI 會議記錄整理）：
    *   ❌ *虛胖指標*：AI 會議記錄功能點擊率（僅反映好奇心，不代表真實轉化）。
    *   ✅ *功能層成功*：每週生成的 AI 會議紀錄中，**在會後 48 小時內被 ≥ 2 位團隊成員瀏覽且完成行動清單勾選** 的比例（反映團隊真正利用此功能進行協作與任務對齊）。
*   **0-to-1 提案嚴禁使用**：在 **0-to-1 全新產品提案中，FSM 必須為 0（不加進簡報）**，因為新產品沒有大盤與子功能之分，引入 FSM 會造成高管觀念混淆。

### 3. 量能指標 (Volume Metric)

*   **定義**：度量漏斗最前端的入口流量與曝光採用次數，用以反映產品的採用規模。
*   **廚房比喻**：**「點擊且採用 AI 主廚推薦的總人數」**（漏斗最上游。如果點的人太少，就主產品無法被拉動）。
*   **設計與稽核原則**：
    *   **使用絕對計數**：量能指標必須是全域加總（如每週採用功能總次數），以避免被少數重度用戶或長 Session 灌歪的平均數。
    *   **硬性採用理由**：必須在簡報中說明此指標如何用來驗證漏斗前端的 Reach 與初步採用規模。
*   **Few-Shot 範例**：
    *   ❌ *易灌歪平均數*：每 Session 使用者平均提問次數。
    *   ✅ *全域加總*：每週總上傳分析的 PDF 文件數量。

### 4. 護欄指標 (Guardrail Metric)

*   **定義**：用於監控品質、安全、用戶疲勞度或系統副作用的防禦指標，用以**排除行為偽裝（防範指標存在被少數重度用戶或短期效應灌歪的風險）**。
*   **廚房比喻**：**「AI 主廚推薦菜的顧客 NPS 滿意度」** 或 **「新菜插入後 5 分鐘內的倒廚餘率/退餐率」**（排除顧客可能因為怕浪費、不好意思剩下而強行吃完的「假成功」）。
*   **設計與稽核原則**：
    *   **NPS 強制配對規則**：如果護欄指標採用了 **NPS (淨推薦值)** 等主觀問卷指標，**AI 必須硬性在旁邊多配對一個「行為日誌指標 (Behavioral Logs Metric)」**（例如：生成後 5 分鐘內的刪除率、人工作業二次修改輪數中位數、或還原率），作為雙重防守。
    *   **不一定是中位數**：中位數只是其中一種形式（如編修次數中位數）。護欄指標可以是用戶滿意度、短時間內的刪除率（Delete Rate）、還原率、或錯誤率。
    *   **可優化的比率/指標**：必須是**可量測、可優化的比率 (0-100%)** 或分數，具備清晰的改進方向，並避開 API 錯誤次數 = 0 等無法灰度迭代的絕對限制。
    *   **硬性採用理由**：必須在簡報中詳細說明此護欄指標是如何防止指標存在被灌歪風險的。
*   **Few-Shot 範例**：
    *   ❌ *絕對值門檻*：API 錯誤次數 = 0（無法衡量過程表現，無法進行灰度優化）。
    *   ✅ *可優化比率*：每週 AI 產出內容的**人工作業修正率**（如修改輪數超過 5 次的比例 ≦ 10%）。
    *   ❌ *偽問題*：系統未斷線率（若基礎建設已保證 99.9% 穩定，此指標無業務優化空間）。
    *   ✅ *品質護欄*：Verifier Agent 判定引用文獻 (Citations) 為 verified 的比例 ≧ 95%（直接為財務級審計把關品質）。
```

- [ ] **Step 3: Verify Module 1 renders with no leftover placeholder**

Run: `grep -n "本節內容於本任務填入" "templates/_shared-modules.md"`
Expected: no match (empty output, exit code 1).

- [ ] **Step 4: Replace the metrics section in `1_to_n_slide_prompt_template.md`**

Find the section starting at `## 📊 指標定義與 Few-Shot 指引 (Metrics Blueprint & Few-Shots)` and ending right before `## 第一階段：主產品定位與指標對齊 (5-Agent Consensus & Warning)`. Replace the entire block (from the `## 📊` heading through the last `✅ *品質護欄*...` bullet, i.e. original lines 42-93) with:

```markdown
## 📊 指標定義與 Few-Shot 指引 (Metrics Blueprint & Few-Shots)

<!-- SYNC: _shared-modules.md#module-1-指標定義與-few-shot -->

指標稽核官與生成引擎必須嚴格使用以下定義、Few-Shot 範例與設計理由規範來處理簡報中的指標（本節與 0-to-1 template 共用，來源見 `_shared-modules.md` Module 1；1-to-N 專屬保留 FSM 章節）：

### 1. 產品北極星指標 (Product North Star Metric - NSM)
*   **定義**：度量產品核心價值向用戶兌現的單一領先指標。必須站在**需求面（用戶感受到的價值）**，代表用戶「真的體驗到價值」的最直接、最誠實的代理行為。
*   **廚房比喻**：**「每週吃光光盤的總數量」**（吃光代表顧客覺得東西好吃、體驗到食物價值的誠實身體行為；統計上只需數盤子，統計摩擦極低）。
*   **設計與稽核原則**：
    *   **專業敘述要求**：一律使用「產品北極星指標」或「產品北極星指標（價值總量）」。
    *   **價值實現代理**：用戶在系統點擊「生成」不代表感受到價值；必須是「匯出檔案」、「複製內容」或「分享給協作者」等代表內容已被人工檢視且即將進入下一步工作流的動作。
    *   **避開百分比陷阱**：產品北極星指標一律使用**「絕對計數」**，以衡量業務規模與實質用戶價值的總和。避免使用率或百分比。
    *   **硬性採用理由**：在簡報中必須詳細說明為什麼該指標代表核心價值的兌現，並解釋為什麼排除註冊數或營收等未能反映使用者實際感受價值的供給面/落後指標。
*   **Few-Shot 範例**：
    *   ❌ *供給面/未反映使用者價值*：每週 AI 生成 PRD 的總次數（用戶可能生成後立即刪除，未感受到價值）。
    *   ✅ *用戶感受價值*：每週成功 **匯出或分享** 的 AI PRD 總數量（匯出代表內容已通過人工檢視且將進入下一步工作流）。
    *   ❌ *落後/財務*：付費訂閱用戶數（無法指導產品改進的結果指標）。
    *   ✅ *用戶感受價值*：每週有進行內容分享或協作的活躍 workspace 數量。

### 2. 功能層成功指標 (Feature Success Metric - FSM)
*   **定義**：用以量測該特定新增功能模組的採用與核心價值轉化。它必須同時包含**「採用該功能」**與**「體驗到主產品核心價值」**兩個要件，用以證明該功能如何發揮觸媒作用，拉動主產品的產品北極星指標。
*   **廚房比喻**：**「點了『AI 主廚推薦新菜』且吃光的顧客人數」**（同時滿足「點了新菜（採用功能）」且「吃光（核心價值實現）」）。
*   **設計與稽核原則**：
    *   **指標拉動理由**：必須說明此指標如何作為優化槓桿拉動主產品的產品北極星指標 (NSM)。
    *   **避開高摩擦動作**：在實務中，要求團隊成員對摘要進行留言或勾選的門檻極高。因此，改採「除建立者外的團隊瀏覽」作為低摩擦但有效的協作與對齊代理行為。
*   **Few-Shot 範例**（主產品：Notion 平台，其大盤 NSM = 每週活躍協作文件數；新增功能：AI 會議記錄整理）：
    *   ❌ *虛胖指標*：AI 會議記錄功能點擊率（僅反映好奇心，不代表真實轉化）。
    *   ✅ *功能層成功*：每週生成的 AI 會議紀錄中，**在會後 48 小時內被 ≥ 2 位團隊成員瀏覽且完成行動清單勾選** 的比例（反映團隊真正利用此功能進行協作與任務對齊）。

### 3. 量能指標 (Volume Metric)
*   **定義**：度量漏斗最前端的入口流量與曝光採用次數，用以反映產品的採用規模。
*   **廚房比喻**：**「點擊且採用 AI 主廚推薦的總人數」**（漏斗最上游。如果點的人太少，就主產品無法被拉動）。
*   **設計與稽核原則**：
    *   **使用絕對計數**：量能指標必須是全域加總（如每週採用功能總次數），以避免被少數重度用戶或長 Session 灌歪的平均數。
    *   **硬性採用理由**：必須在簡報中說明此指標如何用來驗證漏斗前端的 Reach 與初步採用規模。
*   **Few-Shot 範例**：
    *   ❌ *易灌歪平均數*：每 Session 使用者平均提問次數。
    *   ✅ *全域加總*：每週總上傳分析的 PDF 文件數量。

### 4. 護欄指標 (Guardrail Metric)
*   **定義**：用於監控品質、安全、用戶疲勞度或系統副作用的防禦指標，用以**排除行為偽裝（防範指標存在被灌歪的風險）**。
*   **廚房比喻**：**「AI 主廚推薦菜的顧客 NPS 滿意度」** 或 **「新菜插入後 5 分鐘內的倒廚餘率/退餐率」**（排除顧客可能因為怕浪費、不好意思剩下而強行吃完的「假成功」）。
*   **設計與稽核原則**：
    *   **NPS 強制配對規則**：如果護欄指標採用了 **NPS (淨推薦值)** 等主觀問卷指標，**AI 必須硬性在旁邊多配對一個「行為日誌指標 (Behavioral Logs Metric)」**（例如：生成後 5 分鐘內的刪除率、人工作業二次修改輪數中位數、或還原率），作為雙重防守。
    *   **不一定是中位數**：中位數只是其中一種形式（如編修次數中位數）。護欄指標可以是用戶滿意度、短時間內的刪除率（Delete Rate）、還原率、或錯誤率。
    *   **可優化的比率/指標**：必須是**可量測、可優化的比率 (0-100%)** 或分數，具備清晰的改進方向，並避開 API 錯誤次數 = 0 等無法灰度迭代的絕對限制。
    *   **硬性採用理由**：必須在簡報中詳細說明此護欄指標是如何防止指標被灌歪風險的。
*   **Few-Shot 範例**：
    *   ❌ *絕對值門檻*：API 錯誤次數 = 0（無法衡量過程表現，無法進行灰度優化）。
    *   ✅ *可優化比率*：每週 AI 產出內容的**人工作業修正率**（如修改輪數超過 5 次的比例 ≦ 10%）。
    *   ❌ *偽問題*：系統未斷線率（若基礎建設已保證 99.9% 穩定，此指標無業務優化空間）。
    *   ✅ *品質護欄*：Verifier Agent 判定引用文獻 (Citations) 為 verified 的比例 ≧ 95%（直接為財務級審計把關品質）。
```

- [ ] **Step 5: Replace the metrics section in `0_to_1_slide_prompt_template.md`**

Find the section starting at `## 📊 指標定義與 Few-Shot 指引 (Metrics Blueprint & Few-Shots)` and ending right before `## 第一階段：痛點深度調研與並行搜尋 (10-Agent Fan-Out)` (original lines 42-84). Replace it with the same block as Step 4, **except**:
- Drop the `### 2. 功能層成功指標 (Feature Success Metric - FSM)` subsection entirely.
- In its place insert:

```markdown
### 2. 功能層成功指標 (Feature Success Metric - FSM)
*   **0-to-1 提案嚴禁使用**：在 **0-to-1 全新產品提案中，功能層成功指標 (FSM) 必須為 0（不加進簡報）**，因為新產品沒有大盤與子功能之分，引入 FSM 會造成高管觀念混淆。
```
- Renumber the remaining subsections to `3. 量能指標` → stays `3.`, `4. 護欄指標` → stays `4.` (no renumbering needed — FSM keeps slot 2 as a one-line prohibition rather than being deleted, so the existing 1/2/3/4 numbering in the file is preserved).

- [ ] **Step 6: Verify both templates and the shared file agree on the corrected color-free content (color fix happens in Task 5, not here — this check only confirms text consistency)**

Run: `grep -n "大盤指標" "templates/1_to_n_slide_prompt_template.md" "templates/0_to_1_slide_prompt_template.md"`
Expected: no match — the old unprofessional "大盤指標" phrasing must be fully replaced by "產品北極星指標" (this phrase was already banned by the pre-existing audit rule; Step 4/5 must not reintroduce it outside of the Few-Shot 廚房比喻 wording, which doesn't use it).

- [ ] **Step 7: Commit**

```bash
git add templates/_shared-modules.md templates/1_to_n_slide_prompt_template.md templates/0_to_1_slide_prompt_template.md
git commit -m "refactor: extract shared metrics module into _shared-modules.md

Removes duplicated NSM/FSM/Volume/Guardrail definitions from both
slide prompt templates in favor of a synced shared source, and
replaces informal audit vocabulary (虛胖/大盤指標) with professional
phrasing in the Few-Shot examples themselves."
```

---

## Task 2: Confidence-tiered clarification (replaces the "5-Agent virtual consensus" mechanism)

**Files:**
- Modify: `templates/_shared-modules.md` (Module 2 stub)
- Modify: `templates/1_to_n_slide_prompt_template.md` (§"第一階段：主產品定位與指標對齊 (5-Agent Consensus & Warning)")
- Modify: `templates/0_to_1_slide_prompt_template.md` (§"第一階段：痛點深度調研與並行搜尋 (10-Agent Fan-Out)")

**Interfaces:**
- Consumes: nothing new.
- Produces: a "Low confidence → stop and ask, batched, ≤5 questions, anchor+confirm" clarification block that both templates' downstream sections (storyline drafting) can assume has already run before Slide drafting begins.

### Steps

- [ ] **Step 1: Fill in Module 2 in `_shared-modules.md`**

Replace `（Task 2 補上）` under `## Module 2: 信心分級澄清機制` with:

```markdown
> **適用範圍**：兩份 template 共用此機制的骨架（信心自評 → 分級動作），但**欄位清單依
> template 不同而不同**（見下方兩個變體）。此機制**取代**舊版「5 隻虛擬 Agent 共識會議 +
> 事後警告標籤」——虛擬共識會議本質是用更多推論掩蓋推論不足的問題，不構成真正的澄清；
> 信心分級 + 停止提問才是。

### 共用骨架

```text
1. 分析 spec.md 與 plan.md，針對下方欄位清單，各自給出 High / Medium / Low 三級信心：
   - High：文件中有**明確文字**指出答案。
   - Medium：文件中僅有**間接線索**，需要合理推論才能得出答案。
   - Low：文件中**完全沒有**可用線索，任何答案都等同於憑空杜撰。

2. 依信心分級決定動作，二選一：

   A. 若任一欄位為 Low：
      → 立即停止，不產出簡報大綱。一次性列出所有 Low 欄位的澄清問題（最多 5 題），
        每題附上「AI 推論候選值，請確認或修正」（不要用純開放式問句）；問題前先用
        一句話說明為什麼問這個（例如「因為 plan.md 沒提到這個功能屬於哪個產品」）。
        等待使用者回覆後才繼續產出。
      → 使用者可回覆「不用問我，直接用你的推論」跳過此步驟，一律改走 B。

   B. 若為 Medium 或 High：
      → 正常推論並產出完整簡報大綱，但直接寫出推論依據（用一句話說明「根據
        spec.md 第 X 段提到 Y，推論 Z」），並保留現有的警告標籤機制作為次要防線，
        不要用虛擬多 Agent 共識會議這種包裝手法假裝有嚴謹討論過程。
```

### 1-to-N 變體欄位清單（5 項）

1. 這個功能更新附屬的主產品名稱與定位（**注意**：spec.md/plan.md 中出現的 `P1`／`P2`／
   `P3` 等分期用詞，通常代表「同一個新產品的內部功能分期」，**不代表**一定存在既有主產品
   ——不要只因為看到版本化措辭就假設有主產品，這是已知的誤判風險）
2. 主產品現有的北極星指標定義
3. 北極星指標的目前基準值與目標值（數字；若文件只有定義沒有數字，此欄位視為 Low）
4. 這份簡報的受眾與使用場合（面試/內部匯報/對外提案等）
5. 這個功能/專案目前實際進度到哪個階段（規劃中/開發中/已上線；注意 P1-P4 是「規劃分期」
   不等於「實際完成進度」，兩者常被混淆）

### 0-to-1 變體欄位清單（4 項，無需判斷「主產品」因為本質是全新產品）

1. 這個全新產品的一句話定位與核心價值主張
2. 未來承諾的北極星指標定義（0-to-1 天生沒有目前基準值，不需要為此觸發提問）
3. 這份簡報的受眾與使用場合
4. 這個產品目前實際進度到哪個階段（規劃中/開發中/已有 Demo）
```

- [ ] **Step 2: Verify Module 2 has no leftover placeholder**

Run: `grep -n "Task 2 補上" "templates/_shared-modules.md"`
Expected: no match.

- [ ] **Step 3: Replace `第一階段` in `1_to_n_slide_prompt_template.md`**

Find the heading `## 第一階段：主產品定位與指標對齊 (5-Agent Consensus & Warning)` through the end of that section (the three numbered items ending in the `[⚠️ 請在此處更新您正確的主產品名稱及指標]` line, original lines 96-101, right before the `---` separator that precedes `## 第二階段：簡報 Storyline 結構`). Replace with:

```markdown
## 第一階段：主產品定位與指標對齊（信心分級澄清機制）

<!-- SYNC: _shared-modules.md#module-2-信心分級澄清機制（1-to-N 變體） -->

1.  **信心自評**：閱讀 `spec.md` 與 `plan.md`，針對以下 5 個欄位各自給出 High / Medium / Low 信心：
    主產品名稱與定位｜主產品北極星指標定義｜北極星指標目前基準值與目標值｜簡報受眾與使用場合｜目前專案實際進度階段。
    **注意**：文件中出現的 `P1`／`P2`／`P3` 等分期用詞，通常代表「同一個新產品的內部功能分期」，
    不代表一定存在既有主產品——不要只因為看到版本化措辭就假設有主產品。
2.  **依信心分級決定動作**：
    *   任一欄位為 **Low** → 立即停止，不產出簡報大綱。一次性列出所有 Low 欄位的澄清問題（最多 5 題），
        每題附上「AI 推論候選值，請確認或修正」；問題前先用一句話說明為什麼問這個。
        等待使用者回覆後才繼續。使用者可回覆「不用問我，直接用你的推論」跳過此步驟。
    *   全部為 **Medium/High** → 正常推論並產出完整大綱，寫出推論依據（一句話說明根據文件哪處線索），
        並保留下方第 3 點的警告標籤機制作為次要防線。
3.  **提醒與警告標記**：在最終輸出的簡報大綱與講稿中，針對推論出來（Medium/High 信心）的主產品名稱與北極星指標，仍必須**強制在旁加上顯著的警告標記**：
    `[⚠️ 請在此處更新您正確的主產品名稱及指標]`
```

- [ ] **Step 4: Replace `第一階段` in `0_to_1_slide_prompt_template.md`**

Find the heading `## 第一階段：痛點深度調研與並行搜尋 (10-Agent Fan-Out)` through the end of that section (original lines 88-93, right before `## 第二階段：簡報 Storyline 結構`). Replace with:

```markdown
## 第一階段：主產品定位與指標對齊（信心分級澄清機制）＋ 痛點深度調研

<!-- SYNC: _shared-modules.md#module-2-信心分級澄清機制（0-to-1 變體） -->

1.  **信心自評**：閱讀 `spec.md` 與 `plan.md`，針對以下 4 個欄位各自給出 High / Medium / Low 信心：
    產品一句話定位與核心價值主張｜未來承諾的北極星指標定義｜簡報受眾與使用場合｜目前產品實際進度階段。
2.  **依信心分級決定動作**：
    *   任一欄位為 **Low** → 立即停止，不產出簡報大綱。一次性列出所有 Low 欄位的澄清問題（最多 5 題），
        每題附上「AI 推論候選值，請確認或修正」；問題前先用一句話說明為什麼問這個。
        等待使用者回覆後才繼續。使用者可回覆「不用問我，直接用你的推論」跳過此步驟。
    *   全部為 **Medium/High** → 正常推論並產出完整大綱，寫出推論依據，並保留下方警告標籤機制作為次要防線。
3.  **痛點識別**：分析 `spec.md` 中產品欲解決的核心痛點（例如：人工填報耗時、錯誤率高、合規成本等）。
4.  **搜尋策略 (模擬 10 隻平行 Agent)**：自動將該痛點展開為 10 個獨立且具體的搜尋指令，去尋找國內外的權威統計數據與案例。
5.  **數據融入**：你必須在簡報的 **Slide 1 (問題探索)** 放入至少 **2 個真實的量化數據**（包含數據來源與網址連結），以此作為提案說服力的核心支柱。
6.  **提醒與警告標記**：在最終輸出的簡報大綱與講稿中，針對推論出來（Medium/High 信心）的北極星指標，仍必須**強制在旁加上顯著的警告標記**：
    `[⚠️ 請在此處更新您正確的主產品名稱及指標]`
```

- [ ] **Step 5: Verify the old 5-agent / 10-agent framing is gone where it should be**

Run: `grep -n "虛擬 Agent 進行共識探討定調" "templates/1_to_n_slide_prompt_template.md"`
Expected: no match.

Run: `grep -n "信心分級澄清機制" "templates/1_to_n_slide_prompt_template.md" "templates/0_to_1_slide_prompt_template.md"`
Expected: one match per file.

- [ ] **Step 6: Commit**

```bash
git add templates/_shared-modules.md templates/1_to_n_slide_prompt_template.md templates/0_to_1_slide_prompt_template.md
git commit -m "feat: replace 5-agent virtual consensus with confidence-tiered clarification

Low-confidence fields now trigger a single batched, anchor-and-confirm
question round (max 5 questions) instead of a fabricated multi-agent
consensus meeting, per NN/g anchoring-principle and LLM clarification
research. Medium/High confidence keeps inferring but must state its
reasoning instead of role-playing a fake committee."
```

---

## Task 3: Double-auditor upgrade — named agentic patterns + Output Register Guardrail + De-scaffolding

**Files:**
- Modify: `templates/_shared-modules.md` (Module 3 stub)
- Modify: `templates/1_to_n_slide_prompt_template.md` (§"🤖 智能體設計模式執行指南", §"雙重稽核官關卡", the storyline-section opening, the "大盤北極星指標" leftover — n/a for this file — and the "雙重稽核官關卡報告" table in the output format)
- Modify: `templates/0_to_1_slide_prompt_template.md` (same sections, plus the "大盤北極星指標" leftover fix in its storyline section)

**Interfaces:**
- Consumes: none new.
- Produces: a 5-green-light auditor standard (was 3) that the output-format audit table in both templates must report against, plus a de-scaffolding writing principle that governs how Task 4/Task 6's content-drafting instructions should be written (avoid raw analysis-framework display, use single-conclusion-sentence titles).

### Steps

- [ ] **Step 1: Fill in Module 3 in `_shared-modules.md`**

Replace `（Task 3 補上）` under `## Module 3: 雙重稽核官規則` with:

```markdown
> **理論依據**：本規則對應具名的 agentic design pattern（來源：
> `agentic-design-patterns` repo Ch.4 Reflection、Ch.6 Planning、Ch.7 Multi-Agent
> Collaboration、Ch.13 Human-in-the-Loop）：
> - 生產者／評審者角色分離，避免同一套生成邏輯自我審查時的認知偏差（Reflection）。
> - 評審意見衝突時走 Debate & Consensus，而非直接採信任一方（Multi-Agent Collaboration）。
> - 大綱先產出骨架再產出全文，用強制輸出格式取代語言指令（Planning）。
> - 稽核觸發條件用具體情境枚舉，不是模糊的「信心不足時」（Human-in-the-Loop）。

### 執行架構總覽（放在「🤖 智能體設計模式執行指南」章節開頭）

```text
本 prompt 採用**提示鏈（Prompt Chaining Pattern）**設計：將「產出一份稽核過的簡報」拆解
為一系列有明確依賴關係的子步驟，前一步的輸出是後一步的必要輸入，禁止跳步或合併步驟。

本 prompt 的步驟順序是**固定工作流（Fixed Workflow）**而非開放式動態規劃，因為簡報稽核
的「方法」已經是已知且固定的套路，不需要 LLM 自行摸索執行路徑。

在「草擬大綱」步驟中，採用強制型雙段輸出格式（Planning Pattern）：先輸出「### 大綱骨架」
（條列式，各頁核心論點），再輸出「### 完整內容」，避免邊寫邊想導致結構鬆散。
```

### 雙重稽核官的理論基礎（放在雙重稽核官關卡章節開頭）

```text
本 prompt 要求你在同一次生成中，依序扮演三個角色分離、身份互斥的智能體人格：
「草擬者（Producer）」→「稽核官 A：指標稽核官」→「稽核官 B：PM 總監稽核官」。這個設計
對應 Reflection Pattern：評審與產出角色必須分離，以避免同一套生成邏輯自我審查時的認知
偏差。兩位稽核官必須被賦予互斥且明確的評估標準，不是「請再檢查一次」這種模糊指令。

若兩位稽核官對同一頁面有衝突意見，進入 Debate & Consensus：雙方各陳述理由，草擬者需
綜合裁決並記錄裁決依據，而非直接採信任一方。

每輪稽核必須有明確的停止信號（兩位稽核官皆回覆 PASS），最多執行 2 輪；超過則標記為
「需人工判斷」並列出未解決爭議點，避免無限迴圈與 token 浪費。
```

### 第 4 綠燈：專業語域防護（Output Register Guardrail）— 加入 PM 總監稽核官清單

```text
`🟢` **專業語域防護**：以下詞彙**僅限本 prompt 內部推理與稽核說明使用**，**嚴禁出現在
最終輸出的簡報大綱、Slide 標題、條列內容、演講稿之中**（任何形式，包含加引號、加註解）：
「自嗨」「虛胖」「腦補」「洗版」「灌水」及其他口語化/非正式評判詞。若稽核官發現這些
詞彙滲透到對外可見的簡報文字，必須立即改寫為專業敘述後才能通過（例如：「自嗨指標」→
「未能反映使用者實際感受價值的供給面指標」；「指標虛胖」→「指標存在被少數重度用戶或
短期效應灌歪的風險」）。
```

### 拆鷹架寫作原則（放在「簡報 Storyline 結構」章節開頭）＋ 第 5 綠燈

> **來源**：`pm_proposal_presentation.pptx` Slide 3「REMOVE SCAFFOLDING NOISE / 排除框架
> 噪音」——鷹架（分析框架如雙鑽石模型、Persona、共情圖）是團隊內部梳理思路的工具，
> 房子蓋好時輔助用的鷹架就必須拆除，不該把分析框架本身當成簡報內容端給觀眾看。

```text
任何頁面若涉及使用者研究或痛點佐證，**嚴禁**以「空白分析框架」呈現內容（例如完整的
共情圖版面、雙鑽石模型圖、標準 Persona 卡片模板、放滿無關生活細節的用戶側寫）。改為
兩個具體策略（NN/g 去鷹架化建議）：

1.  **呈現洞察，隱藏模版**：不展示分析框架本身，直接引用一句最具代表性的使用者痛點
    原話或具體情境描述，把「洞察結論」推到最前面。
2.  **單一結論句標題**：所有 Slide 標題禁止使用「目錄名詞」（如「使用者訪談」「現狀
    分析」「Persona 側寫」），必須改寫為一句完整的結論主張。
```

```text
`🟢` **拆鷹架與洞察優先**：檢查是否有任何頁面殘留「空白分析框架」或「目錄名詞標題」。
若發現，需改寫為具體洞察引述與結論句標題後才能通過。
```
```

- [ ] **Step 2: Verify Module 3 has no leftover placeholder**

Run: `grep -n "Task 3 補上" "templates/_shared-modules.md"`
Expected: no match.

- [ ] **Step 3: Update `1_to_n_slide_prompt_template.md`'s "🤖 智能體設計模式執行指南" section**

Find the heading `## 🤖 智能體設計模式執行指南 (Agentic Design Patterns Execution)` and the subsection `### 1. 執行路徑規劃 (Planning & Chaining Phase)` that immediately follows it (original lines 14-24, ending right before `### 2. 雙重稽核官關卡 (Double-Auditor Gatekeeper)`). Insert the following new subsection between the `## 🤖 智能體設計模式執行指南` heading and the existing `### 1. 執行路徑規劃` subsection (do not delete `### 1.` — it stays as-is):

```markdown
## 🤖 智能體設計模式執行指南 (Agentic Design Patterns Execution)

<!-- SYNC: _shared-modules.md#module-3-雙重稽核官規則 -->（執行架構總覽段落）

本 prompt 採用**提示鏈（Prompt Chaining Pattern）**設計：將「產出一份稽核過的簡報」這個複雜任務拆解為一系列有明確依賴關係的子步驟，前一步的輸出是後一步的必要輸入，禁止跳步或合併步驟。

本 prompt 的步驟順序是**固定工作流（Fixed Workflow）**而非開放式動態規劃（Planning Pattern 的自主路徑發現），因為簡報稽核的「方法」已經是已知且固定的套路（分析 → 澄清 → 草擬 → 雙重稽核 → 輸出），不需要 LLM 自行摸索執行路徑；固定工作流比動態規劃更可預測、更適合品質優先於彈性的場景。

在「草擬大綱」步驟中，請採用強制型雙段輸出格式，確保先規劃、再產出：先輸出「### 大綱骨架」（條列式，各頁核心論點與資料來源對應），再輸出「### 完整內容」。此設計來自 Planning Pattern 中「用預定義輸出結構強制先規劃後執行」的做法，避免 LLM 邊寫邊想導致結構鬆散。

為了確保產出簡報的高品質與指標的絕對嚴謹性，你（執行此 Prompt 的 LLM）必須依照以下 **提示鏈、多角色稽核與反思規劃 (Prompt Chaining, Reflection Pattern, Multi-Agent Collaboration)** 順序執行：
```

- [ ] **Step 4: Update `1_to_n_slide_prompt_template.md`'s "雙重稽核官關卡" opener and add the 4th green light**

Find the heading `### 2. 雙重稽核官關卡 (Double-Auditor Gatekeeper)` and the sentence immediately after it (`你必須虛擬分身為兩位最嚴苛的審查官，逐頁進行對抗性稽核。若未通過，必須指出缺陷 (Gap)、修改內容、並重新進行稽核直至過關：`). Insert the Reflection-theory paragraph between the heading and that sentence:

```markdown
### 2. 雙重稽核官關卡 (Double-Auditor Gatekeeper)

<!-- SYNC: _shared-modules.md#module-3-雙重稽核官規則 -->（理論基礎段落）

本 prompt 要求你在同一次生成中，依序扮演三個角色分離、身份互斥的智能體人格：「草擬者（Producer）」→「稽核官 A：指標稽核官」→「稽核官 B：PM 總監稽核官」。這個設計對應 Reflection Pattern：評審與產出角色必須分離，以避免同一套生成邏輯自我審查時的認知偏差。兩位稽核官必須被賦予互斥且明確的評估標準，不是「請再檢查一次」這種模糊指令。

若兩位稽核官對同一頁面有衝突意見，進入 Debate & Consensus：雙方各陳述理由，草擬者需綜合裁決並記錄裁決依據，而非直接採信任一方。每輪稽核必須有明確的停止信號（兩位稽核官皆回覆 PASS），最多執行 2 輪；超過則標記為「需人工判斷」並列出未解決爭議點，避免無限迴圈與 token 浪費。

你必須虛擬分身為兩位最嚴苛的審查官，逐頁進行對抗性稽核。若未通過，必須指出缺陷 (Gap)、修改內容、並重新進行稽核直至過關：
```

Then, in the same section, under `#### 👤 PM 總監稽核官 (PM Director Audit Officer)`, immediately after the existing 3rd green light (`3.  \`🟢\` **警告標籤與定義**：...`), append a 4th AND 5th green light:

```markdown
    4.  `🟢` **專業語域防護**：以下詞彙僅限本 prompt 內部推理與稽核說明使用，嚴禁出現在最終輸出的簡報大綱、Slide 標題、條列內容、演講稿之中（任何形式，包含加引號、加註解）：「自嗨」「虛胖」「腦補」「洗版」「灌水」及其他口語化/非正式評判詞。若發現這些詞彙滲透到對外可見的簡報文字，必須立即改寫為專業敘述後才能通過（例如：「自嗨指標」→「未能反映使用者實際感受價值的供給面指標」）。
    5.  `🟢` **拆鷹架與洞察優先**：檢查是否有任何頁面殘留「空白分析框架」（如完整的共情圖版面、雙鑽石模型圖、標準 Persona 卡片模板）或「目錄名詞標題」（如「使用者訪談」「現狀分析」）。若發現，需改寫為具體洞察引述與結論句標題後才能通過。
```

- [ ] **Step 5: Repeat Steps 3-4 for `0_to_1_slide_prompt_template.md`**

Same insertions, same anchor text, applied to `0_to_1_slide_prompt_template.md`'s own `## 🤖 智能體設計模式執行指南` / `### 2. 雙重稽核官關卡` sections (its own original lines 14-39). The 0-to-1 template's PM Director auditor already has exactly 3 green lights ending in a "主管視角與名詞定義" item — append the same 4th and 5th green light block after it.

- [ ] **Step 6: Insert the de-scaffolding writing principle at the top of the storyline section in both templates**

In `templates/1_to_n_slide_prompt_template.md`, find:

```markdown
## 第二階段：簡報 Storyline 結構 (1-to-N 功能更新專用)

既有產品功能更新簡報大綱必須嚴格遵循以下 **7 頁結構**，以指標驅動故事線：
```

Replace with:

```markdown
## 第二階段：簡報 Storyline 結構 (1-to-N 功能更新專用)

<!-- SYNC: _shared-modules.md#module-3-雙重稽核官規則 -->（拆鷹架寫作原則段落）

任何頁面若涉及使用者研究或痛點佐證，**嚴禁**以「空白分析框架」呈現內容（例如完整的共情圖版面、雙鑽石模型圖、標準 Persona 卡片模板、放滿無關生活細節的用戶側寫）。改為兩個具體策略（NN/g 去鷹架化建議）：

1.  **呈現洞察，隱藏模版**：不展示分析框架本身，直接引用一句最具代表性的使用者痛點原話或具體情境描述，把「洞察結論」推到最前面。
2.  **單一結論句標題**：所有 Slide 標題禁止使用「目錄名詞」（如「使用者訪談」「現狀分析」「Persona 側寫」），必須改寫為一句完整的結論主張。

既有產品功能更新簡報大綱必須嚴格遵循以下 **7 頁結構**，以指標驅動故事線：
```

In `templates/0_to_1_slide_prompt_template.md`, find:

```markdown
## 第二階段：簡報 Storyline 結構 (0-to-1 全新產品專用)

全新產品簡報大綱必須嚴格遵循以下 **6 頁結構**，模仿熟成提案的說服邏輯：
```

Replace with:

```markdown
## 第二階段：簡報 Storyline 結構 (0-to-1 全新產品專用)

<!-- SYNC: _shared-modules.md#module-3-雙重稽核官規則 -->（拆鷹架寫作原則段落）

任何頁面若涉及使用者研究或痛點佐證，**嚴禁**以「空白分析框架」呈現內容（例如完整的共情圖版面、雙鑽石模型圖、標準 Persona 卡片模板、放滿無關生活細節的用戶側寫）。改為兩個具體策略（NN/g 去鷹架化建議）：

1.  **呈現洞察，隱藏模版**：不展示分析框架本身，直接引用一句最具代表性的使用者痛點原話或具體情境描述，把「洞察結論」推到最前面。
2.  **單一結論句標題**：所有 Slide 標題禁止使用「目錄名詞」（如「使用者訪談」「現狀分析」「Persona 側寫」），必須改寫為一句完整的結論主張。

全新產品簡報大綱必須嚴格遵循以下 **6 頁結構**，模仿熟成提案的說服邏輯：
```

- [ ] **Step 7: Fix the leftover informal "大盤北極星指標" phrasing in `0_to_1_slide_prompt_template.md`'s storyline section**

Find (in the `## Slide 5: [第五頁標題 - 未來指標承諾]` bullet list inside the storyline section, not the Gamma-prompt output block):

```markdown
    *   *內容*：定義大盤北極星指標 (NSM)（例如週匯出量），**附帶明確的「採用理由與商業價值理由」**。
```

Replace with:

```markdown
    *   *內容*：定義產品北極星指標 (NSM)（例如週匯出量），**附帶明確的「採用理由與商業價值理由」**。
```

This is pre-existing informal phrasing outside Task 1's scope (Task 1 only touched the Metrics Blueprint section); fixing it now keeps it consistent with the Output Register Guardrail's spirit even though "大盤北極星指標" isn't literally one of the five banned words.

- [ ] **Step 8: Update the audit-report table header comment in both templates' 輸出格式 section**

In both files, find the line `### 雙重稽核官關卡報告 (Audit Reports)` and the table immediately below it. Add one sentence directly under the heading, before the table:

```markdown
### 雙重稽核官關卡報告 (Audit Reports)

> 表格中的「PM 總監稽核官評審」欄位必須涵蓋全部 5 個綠燈（含第 4 項專業語域防護、第 5 項拆鷹架與洞察優先），不是原本的 3 個。
```

(Leave the table itself unchanged — the `🟢🟢🟢` markers in the existing rows are illustrative placeholders the LLM fills in at generation time, not something this plan edits; the sentence above is what raises the bar to 5 checks.)

- [ ] **Step 9: Verify the 4th and 5th green lights exist in both templates, and the leftover phrasing is fixed**

Run: `grep -c "專業語域防護" "templates/1_to_n_slide_prompt_template.md" "templates/0_to_1_slide_prompt_template.md"`
Expected: `templates/1_to_n_slide_prompt_template.md:2` and `templates/0_to_1_slide_prompt_template.md:2` (once in the auditor rule, once in the table note).

Run: `grep -c "拆鷹架" "templates/1_to_n_slide_prompt_template.md" "templates/0_to_1_slide_prompt_template.md"`
Expected: `templates/1_to_n_slide_prompt_template.md:3` and `templates/0_to_1_slide_prompt_template.md:3` (once in the storyline-opening block, once in the auditor 5th green light, once in the table note).

Run: `grep -n "大盤北極星指標\|大盤 NSM" "templates/1_to_n_slide_prompt_template.md" "templates/0_to_1_slide_prompt_template.md"`
Expected: no match.

- [ ] **Step 10: Commit**

```bash
git add templates/_shared-modules.md templates/1_to_n_slide_prompt_template.md templates/0_to_1_slide_prompt_template.md
git commit -m "feat: name the agentic patterns behind the double-auditor mechanism

Ties Prompt Chaining / Planning / Reflection / Multi-Agent Collaboration
patterns to the existing chaining and audit steps, adds a 4th green-light
check (Output Register Guardrail) barring informal audit vocabulary
(自嗨/虛胖/腦補) from leaking into generated slide content, and adds a
5th green-light check plus a storyline-opening writing rule (De-scaffolding,
from pptx Slide 3) requiring insight-first content and single-conclusion-
sentence titles instead of raw analysis-framework slides."
```

---

## Task 4: Cover slide (Slide 0) formula

**Files:**
- Modify: `templates/_shared-modules.md` (Module 4 stub)
- Modify: `templates/1_to_n_slide_prompt_template.md` (§"第二階段：簡報 Storyline 結構" and the 輸出格式 Gamma prompt block)
- Modify: `templates/0_to_1_slide_prompt_template.md` (same)

**Interfaces:**
- Consumes: none new.
- Produces: a `## Slide 0: ...` block that must appear before `## Slide 1` in both templates' Gamma-prompt output format.

### Steps

- [ ] **Step 1: Fill in Module 4 in `_shared-modules.md`**

Replace `（Task 4 補上）` under `## Module 4: 標題頁公式` with:

```markdown
> **來源**：`pm_proposal_presentation.pptx` Slide 1/10/18 實測版式（封面頁與章節分節頁
> 共用同一版面公式）。

```markdown
## 第○階段：標題頁 / 封面頁規格（Cover Slide Specification）

在正式的大綱**之前**，必須額外生成一頁獨立的「Slide 0：封面頁」，作為整份簡報的開場：

*   **版面公式**：
    *   全頁滿版背景色（暖米白 `#FDFCFA`）。
    *   左側靠邊裝飾雙線（一粗一細的垂直線條，貼齊左邊界，幾乎頂滿全頁高度，營造書脊/裝訂感）。
    *   右上角與右下偏中各放一個大小不同的裝飾圓形色塊（大圓在右下、較小圓在右上，兩者不對稱錯位），使用 Brand Highlight 淡色調。
    *   文字內容一律靠左對齊，垂直排列，由上到下依序為：
        1.  Overline（英文全大寫分類詞，小字級、Brand Strong Teal `#007583`）
        2.  H1 主標題（可分 2-3 行的結論句/價值主張，大字級、Primary Navy 或 Deep Charcoal）
        3.  一句話副標說明（中等字級、次文字灰 `#525864`）
        4.  作者/單位落款（小字級、次文字灰 `#525864`，置於頁面下方）

### 對應 Gamma Prompt 輸出格式（插入大綱最前方）：

\`\`\`text
## Slide 0: [封面標題]
*   Layout: Title cover slide with asymmetric decorative circles (top-right
    small circle, bottom-right large circle) and a vertical double-line
    accent on the far left edge, spanning nearly full page height.
*   Overline (small caps, teal #007583): [PROJECT CATEGORY] PROPOSAL
*   H1 (large, 2-3 lines, navy #153166): [一句話核心主張，倒金字塔結論句]
*   Subtitle (medium, gray #525864): [一句話說明簡報目的]
*   Byline (small, gray #525864, bottom-left): [提案人] · [職稱] · [簡報用途]
\`\`\`
```
```

- [ ] **Step 2: Verify Module 4 has no leftover placeholder**

Run: `grep -n "Task 4 補上" "templates/_shared-modules.md"`
Expected: no match.

- [ ] **Step 3: Add the cover-slide stage to `1_to_n_slide_prompt_template.md`'s storyline section**

Find the heading `## 第二階段：簡報 Storyline 結構 (1-to-N 功能更新專用)` and insert a new stage directly **before** it:

```markdown
## 第 1.5 階段：標題頁 / 封面頁規格（Cover Slide Specification）

<!-- SYNC: _shared-modules.md#module-4-標題頁公式 -->

在正式的 7 頁大綱**之前**，必須額外生成一頁獨立的「Slide 0：封面頁」，作為整份簡報的開場：

*   **版面公式**：
    *   全頁滿版背景色（暖米白 `#FDFCFA`）。
    *   左側靠邊裝飾雙線（一粗一細的垂直線條，貼齊左邊界，幾乎頂滿全頁高度，營造書脊/裝訂感）。
    *   右上角與右下偏中各放一個大小不同的裝飾圓形色塊（大圓在右下、較小圓在右上，兩者不對稱錯位），使用 Brand Highlight 淡色調。
    *   文字內容一律靠左對齊，垂直排列，由上到下依序為：
        1.  Overline（英文全大寫分類詞，小字級、Brand Strong Teal `#007583`）
        2.  H1 主標題（可分 2-3 行的結論句/價值主張，大字級、Primary Navy 或 Deep Charcoal）
        3.  一句話副標說明（中等字級、次文字灰 `#525864`）
        4.  作者/單位落款（小字級、次文字灰 `#525864`，置於頁面下方）

## 第二階段：簡報 Storyline 結構 (1-to-N 功能更新專用)
```

- [ ] **Step 4: Add `## Slide 0` to the Gamma-prompt output block in `1_to_n_slide_prompt_template.md`**

Find the line `# [簡報標題]` inside the fenced ` ```text ` Gamma prompt block (the one starting with `--- START OF GAMMA PROMPT ---`), and the `## Slide 1: [第一頁標題 - 項目現狀]` heading right after it. Insert between them:

```markdown
# [簡報標題]

## Slide 0: [封面標題]
*   Layout: Title cover slide with asymmetric decorative circles (top-right small circle, bottom-right large circle) and a vertical double-line accent on the far left edge, spanning nearly full page height.
*   Overline (small caps, teal #007583): [PROJECT CATEGORY] PROPOSAL
*   H1 (large, 2-3 lines, navy #153166): [一句話核心主張，倒金字塔結論句]
*   Subtitle (medium, gray #525864): [一句話說明簡報目的]
*   Byline (small, gray #525864, bottom-left): [提案人] · [職稱] · [簡報用途]

## Slide 1: [第一頁標題 - 項目現狀]
```

- [ ] **Step 5: Repeat Steps 3-4 for `0_to_1_slide_prompt_template.md`**

Same insertion, adapted: insert `## 第 1.5 階段` before `## 第二階段：簡報 Storyline 結構 (0-to-1 全新產品專用)`, and insert the `## Slide 0: [封面標題]` block before `## Slide 1: [第一頁標題 - 問題探索]` inside its Gamma prompt block.

- [ ] **Step 6: Verify Slide 0 precedes Slide 1 in both templates**

Run: `grep -n "^## Slide 0\|^## Slide 1:" "templates/1_to_n_slide_prompt_template.md" "templates/0_to_1_slide_prompt_template.md"`
Expected: for each file, the `## Slide 0` line number is smaller than the `## Slide 1:` line number.

- [ ] **Step 7: Commit**

```bash
git add templates/_shared-modules.md templates/1_to_n_slide_prompt_template.md templates/0_to_1_slide_prompt_template.md
git commit -m "feat: add cover slide (Slide 0) formula to both templates

Reproduces the pptx reference deck's cover/section-divider layout
(asymmetric decorative circles, left spine double-line, overline/H1/
subtitle/byline stack) as a mandatory Slide 0 before the main outline."
```

---

## Task 5: Gamma style directives — color fix, footer/overline, Brand Kit note, post-gen checklist, Outline-first tip

**Files:**
- Modify: `templates/_shared-modules.md` (Module 5 stub)
- Modify: `templates/1_to_n_slide_prompt_template.md` (§"第三階段：Gamma 設計與風格指令" and its corresponding `### 🎨 Design & Style Directives for Gamma:` block inside 輸出格式)
- Modify: `templates/0_to_1_slide_prompt_template.md` (same)

**Interfaces:**
- Consumes: none new.
- Produces: corrected color tokens (`#007583` replacing `#48B7BD`, new `#525864` secondary gray) referenced consistently by Task 6's Mermaid module.

### Steps

- [ ] **Step 1: Fill in Module 5 in `_shared-modules.md`**

Replace `（Task 5 補上）` under `## Module 5: Gamma 風格精簡指令` with:

```markdown
> **來源**：Gamma AI 能力調研（結論：Gamma 不會解析文字 prompt 裡的 hex 色碼與 inline
> SVG，色彩/字體應透過 Theme Editor / Brand Kit 一次性設定；風格指令應精簡為高層基調宣告）
> ＋ pptx 落差分析（強調色實測為 `#007583`，非原用的 `#48B7BD`；缺次文字灰、頁尾、Overline）。

```markdown
## 第三階段：Gamma 設計與風格指令 (Gamma Style Directives)

在生成的 Prompt 底部，必須附帶一組**精簡的風格制約**，以便直接複製到 Gamma 中：

1.  **主題基調 (Theme)**：Minimalist visual style, large typography, high contrast,
    airy layout with generous padding and margins (breathing room), based on
    `design-system-portfolio-site_6640.md`.
2.  **配色方案 (Colors)**（僅列高層基調，精確色碼透過下方「Brand Kit 一次性設定」落實）：
    *   頁面背景：暖米白 Warm Paper White (`#FDFCFA`)
    *   主標題與卡片框：深靛藍 Classic Navy (`#153166`)
    *   高亮強調／Overline／icon：深青 Brand Strong Teal (`#007583`)（**不是**
        `#48B7BD`——那個色階只適合低透明度背景光暈，不適合前景文字/icon）
    *   次要強調（可選，次要 icon/次標題）：中青 (`#00969D`)
    *   主內文：深炭黑 Deep Charcoal (`#171C24`)
    *   次文字/輔助說明：石墨灰 Slate Gray (`#525864`)（新增；用於卡片說明文字、
        頁尾、輔助標籤等非主要強調的文字內容）
    *   警示/痛點：猩紅 Rose Crimson (`#B91C1C`)
3.  **排版限制 (Layout Constraints)**：
    *   嚴格禁止任何 Emoji（如 ↗, ✅ 等），使用 Unicode 標點（如 `—`, `·`）或文字代替。
    *   排版極度要求呼吸感，禁止擁擠。
    *   採用「大數字 KPI 卡片」呈現首頁數據。
    *   使用「2欄/3欄拆分卡片」呈現用戶痛點與成功定義，代替長文字條列。
    *   **頁尾格式（每頁皆須有）**：頁面左下角固定顯示 `[簡報系列名稱英文] · PAGE [兩位數頁碼]`，
        字級極小，顏色為次文字灰 `#525864`。
    *   **Overline / Eyebrow（每頁標題上方皆須有）**：在 H1 標題正上方加一行全大寫英文
        分類詞，字級小、顏色使用 Brand Strong Teal `#007583`，用於標示這一頁在敘事鏈中
        的主題分類。
4.  **文字密度 (Text Density)**：Brief（物理簡練、視覺主導）。

### Brand Kit 一次性設定指引（非每次生成都要重複）

Gamma 不會可靠解析文字 prompt 裡的 hex 色碼與字體宣告——這些設定應透過 Gamma 的
**Theme Editor / Brand Kit** 介面一次性設定（色彩、字體、Logo），之後生成的每份簡報自動
套用，不需要每次都在文字 prompt 裡重複列出精確色碼。文字 prompt 只需保留「延用品牌
Navy+Teal 配色」這類高層基調宣告即可。

### 生成後檢查清單（取代對 Gamma 一次到位的期待）

Gamma 對精細視覺規則（emoji 禁用、精確色階、字級層級）的遵循度不保證一次到位。
使用者貼上 Prompt 生成後，應人工巡檢以下項目：
*   [ ] 是否有 Emoji 混入
*   [ ] 強調色是否偏離 Navy/Teal 基調
*   [ ] 是否有頁面資訊過度擁擠
*   [ ] 頁尾與 Overline 是否每頁一致

### Outline-first 使用提醒

貼上 Prompt 後，Gamma 會先產出一份中間大綱供審閱。**請先確認大綱結構無誤，再按下
「生成完整簡報」**——修正大綱結構遠比事後重寫整份簡報的內容便宜，這是 Gamma 官方
認可的效率作法。
```
```

- [ ] **Step 2: Verify Module 5 has no leftover placeholder**

Run: `grep -n "Task 5 補上" "templates/_shared-modules.md"`
Expected: no match.

- [ ] **Step 3: Replace `第三階段` in `1_to_n_slide_prompt_template.md`**

Find the heading `## 第三階段：Gamma 設計與風格指令 (Gamma Style Directives)` through the end of that section (original lines 136-154, ending right before `---` / `## 輸出格式`). Replace with the Module 5 content from Step 1, prefixed with the sync tag:

```markdown
## 第三階段：Gamma 設計與風格指令 (Gamma Style Directives)

<!-- SYNC: _shared-modules.md#module-5-gamma-風格精簡指令 -->

在生成的 Prompt 底部，必須附帶一組**精簡的風格制約**，以便直接複製到 Gamma 中：

1.  **主題基調 (Theme)**：Minimalist visual style, large typography, high contrast, airy layout with generous padding and margins (breathing room), based on `design-system-portfolio-site_6640.md`.
2.  **配色方案 (Colors)**（僅列高層基調，精確色碼透過下方「Brand Kit 一次性設定」落實）：
    *   頁面背景：暖米白 Warm Paper White (`#FDFCFA`)
    *   主標題與卡片框：深靛藍 Classic Navy (`#153166`)
    *   高亮強調／Overline／icon：深青 Brand Strong Teal (`#007583`)（**不是** `#48B7BD`——那個色階只適合低透明度背景光暈，不適合前景文字/icon）
    *   次要強調（可選，次要 icon/次標題）：中青 (`#00969D`)
    *   主內文：深炭黑 Deep Charcoal (`#171C24`)
    *   次文字/輔助說明：石墨灰 Slate Gray (`#525864`)（新增；用於卡片說明文字、頁尾、輔助標籤等非主要強調的文字內容）
    *   警示/痛點：猩紅 Rose Crimson (`#B91C1C`)
3.  **排版限制 (Layout Constraints)**：
    *   嚴格禁止任何 Emoji（如 ↗, ✅ 等），使用 Unicode 標點（如 `—`, `·`）或文字代替。
    *   排版極度要求呼吸感，禁止擁擠。
    *   採用「大數字 KPI 卡片」呈現 Slide 1 的數據。
    *   使用「2欄/3欄拆分卡片」呈現用戶痛點與成功定義，代替長文字條列。
    *   **頁尾格式（每頁皆須有）**：頁面左下角固定顯示 `[簡報系列名稱英文] · PAGE [兩位數頁碼]`，字級極小，顏色為次文字灰 `#525864`。
    *   **Overline / Eyebrow（每頁標題上方皆須有）**：在 H1 標題正上方加一行全大寫英文分類詞，字級小、顏色使用 Brand Strong Teal `#007583`，用於標示這一頁在敘事鏈中的主題分類。
    *   **資料視覺化流程圖與架構圖**：見下方「第四階段：流程圖策略」，不再使用 SVG/CSS 語法。
4.  **文字密度 (Text Density)**：Brief（物理簡練、視覺主導）。

### Brand Kit 一次性設定指引（非每次生成都要重複）

Gamma 不會可靠解析文字 prompt 裡的 hex 色碼與字體宣告——這些設定應透過 Gamma 的 **Theme Editor / Brand Kit** 介面一次性設定（色彩、字體、Logo），之後生成的每份簡報自動套用，不需要每次都在文字 prompt 裡重複列出精確色碼。文字 prompt 只需保留「延用品牌 Navy+Teal 配色」這類高層基調宣告即可。

### 生成後檢查清單（取代對 Gamma 一次到位的期待）

Gamma 對精細視覺規則（emoji 禁用、精確色階、字級層級）的遵循度不保證一次到位。使用者貼上 Prompt 生成後，應人工巡檢以下項目：
*   [ ] 是否有 Emoji 混入
*   [ ] 強調色是否偏離 Navy/Teal 基調
*   [ ] 是否有頁面資訊過度擁擠
*   [ ] 頁尾與 Overline 是否每頁一致

### Outline-first 使用提醒

貼上 Prompt 後，Gamma 會先產出一份中間大綱供審閱。**請先確認大綱結構無誤，再按下「生成完整簡報」**——修正大綱結構遠比事後重寫整份簡報的內容便宜，這是 Gamma 官方認可的效率作法。
```

- [ ] **Step 4: Replace the `### 🎨 Design & Style Directives for Gamma:` block inside `1_to_n_slide_prompt_template.md`'s 輸出格式**

Find the block:

```markdown
### 🎨 Design & Style Directives for Gamma:
- **Theme**: Minimalist visual style, large typography, high contrast, airy layout with generous padding and margins (breathing room) based on design-system-portfolio-site_6640.md.
- **Colors**: Background #FDFCFA, Primary Accent #153166, Brand Highlight #48B7BD, Body Text #171C24, Alerts #B91C1C.
- **Constraints**: Strictly forbid all emojis. Keep text density low (Brief). Max 3 items per card.
- **Layouts**: Use large metrics callouts for Slide 1, 2-column split cards for Slide 2 & 4, horizontal connected interaction blocks with SVG arrows for Slide 5 & 6, and a hierarchical connection list for Slide 7.
```

Replace with:

```markdown
### 🎨 Design & Style Directives for Gamma:
- **Theme**: Minimalist visual style, large typography, high contrast, airy layout with generous padding and margins (breathing room) based on design-system-portfolio-site_6640.md.
- **Colors**: Background #FDFCFA, Primary Accent #153166, Brand Strong Teal #007583, Secondary Text #525864, Body Text #171C24, Alerts #B91C1C.
- **Constraints**: Strictly forbid all emojis. Keep text density low (Brief). Every slide must show a footer "[SERIES NAME] · PAGE [NN]" and an overline (small caps, teal) above the H1.
- **Layouts**: Use large metrics callouts for Slide 1, 2-column split cards for Slide 2 & 4, and a hierarchical connection list for Slide 7. Diagrams for Slide 5 & 6 are supplied as pre-rendered Mermaid images (see Stage 4 below) — do not ask Gamma to generate them from scratch.
- **Reminder**: Review Gamma's intermediate outline before generating the full deck (Outline-first) — correcting structure there is cheaper than rewriting slides after generation.
```

- [ ] **Step 5: Repeat Steps 3-4 for `0_to_1_slide_prompt_template.md`**

Same replacement, adapted for its own `### 🎨 Design & Style Directives for Gamma:` block (which references `Slide 2 & 3`, `Slide 4` and `Slide 6` — keep those slide-number references as-is, only change the color line, the emoji/footer/overline constraint line, and the diagram line to match Step 4's wording, and append the same Outline-first reminder line).

- [ ] **Step 6: Verify the old wrong hex is gone and the new one is present**

Run: `grep -n "48B7BD" "templates/1_to_n_slide_prompt_template.md" "templates/0_to_1_slide_prompt_template.md" "templates/_shared-modules.md"`
Expected: no match.

Run: `grep -c "#007583" "templates/1_to_n_slide_prompt_template.md" "templates/0_to_1_slide_prompt_template.md"`
Expected: at least 2 matches in each file (style section + design directives block).

- [ ] **Step 7: Commit**

```bash
git add templates/_shared-modules.md templates/1_to_n_slide_prompt_template.md templates/0_to_1_slide_prompt_template.md
git commit -m "fix: correct Gamma brand accent color and simplify style directives

Replaces the wrong #48B7BD accent with the pptx-verified #007583 Brand
Strong Teal, adds the missing secondary-gray/footer/overline rules,
moves precise hex/font control to a one-time Brand Kit setup note
(Gamma doesn't reliably parse hex from text prompts), and adds a
post-generation checklist plus an Outline-first review reminder."
```

---

## Task 6: Mermaid-based diagram strategy (replaces SVG/CSS flowchart directives)

**Files:**
- Modify: `templates/_shared-modules.md` (Module 6 stub)
- Modify: `templates/1_to_n_slide_prompt_template.md` (Slide 5 & 6 diagram instructions inside 輸出格式, plus the style-section diagram bullet already updated in Task 5)
- Modify: `templates/0_to_1_slide_prompt_template.md` (Slide 4 diagram instructions)

**Interfaces:**
- Consumes: color tokens from Task 5 (`#153166`, `#007583`, `#B91C1C`, `#FDFCFA`).
- Produces: a `## 第四階段：流程圖策略` section with concrete Mermaid syntax templates for both files.

### Steps

- [ ] **Step 1: Fill in Module 6 in `_shared-modules.md`**

Replace `（Task 6 補上）` under `## Module 6: Mermaid 流程圖策略` with:

```markdown
> **來源**：Gamma markdown 格式精確度調研（結論：Gamma 是 AI 生成引擎，不會照抄 markdown
> 版面，也不可靠渲染 inline SVG——寫死版面容易被誤判成資料表格）＋ pptx 落差分析（4 種
> 具體圖形語言：橫向編號步驟卡／Z字型技術管線／指標關係輪盤／漏斗圖）。**放棄**要求
> Gamma 自己畫圖，改為讓 template 直接產出一段 Mermaid 語法，使用者自行用 Mermaid 渲染
> 工具（如 mermaid.live）轉成圖片後手動插入/替換 Gamma 生成頁面對應位置。

```markdown
## 第四階段：流程圖策略（Mermaid 先繪圖，再以圖片插入 Gamma）

不要要求 Gamma 自己生成精確的流程圖/架構圖——Gamma 是 AI 生成引擎，會對輸入做語意
二次詮釋，不保證還原任何精確版面，複雜的 inline SVG/CSS 也不會被渲染。改為：

1.  針對每一頁需要流程圖/架構圖的 Slide，依語意選擇下方其中一種 Mermaid 圖形類型，
    產出**獨立的 Mermaid 程式碼區塊**（不是塞進 Gamma 大綱文字裡）：

    *   **橫向編號步驟卡**（使用者互動流程用）：
        \`\`\`mermaid
        flowchart LR
            A(["1 · 輸入端"]) --> B(["2 · AI 核心處理"]) --> C(["3 · 校對與驗證"]) --> D(["4 · 完成匯出"])
            style A fill:#153166,color:#FDFCFA
            style B fill:#007583,color:#FDFCFA
            style C fill:#007583,color:#FDFCFA
            style D fill:#153166,color:#FDFCFA
        \`\`\`

    *   **Z 字型技術管線圖**（系統架構整合用）：
        \`\`\`mermaid
        flowchart TD
            A["既有系統整合點"] --> B["AI 核心運算層"]
            B --> C["新功能交互介面"]
            C --> D["前後台資料串接"]
            style A fill:#153166,color:#FDFCFA
            style B fill:#007583,color:#FDFCFA
            style C fill:#007583,color:#FDFCFA
            style D fill:#153166,color:#FDFCFA
        \`\`\`

    *   **指標關係輪盤圖**（多指標互相拉動關係用）：
        \`\`\`mermaid
        flowchart TD
            NSM["產品北極星指標"]
            NSM --- FSM["功能層成功指標"]
            NSM --- VOL["量能指標"]
            NSM --- GRD["護欄指標"]
            style NSM fill:#153166,color:#FDFCFA
            style FSM fill:#007583,color:#FDFCFA
            style VOL fill:#525864,color:#FDFCFA
            style GRD fill:#B91C1C,color:#FDFCFA
        \`\`\`

    *   **漏斗圖**（流量流失視覺化用）：
        \`\`\`mermaid
        flowchart TD
            A["曝光/入口流量"] --> B["採用功能"] --> C["完成核心動作"]
            style A fill:#153166,color:#FDFCFA
            style B fill:#007583,color:#FDFCFA
            style C fill:#B91C1C,color:#FDFCFA
        \`\`\`

2.  Mermaid 圖表顏色**必須**遵守 `design-system-portfolio-site_6640.md` 的色彩 token：
    Primary Navy `#153166`、Brand Strong Teal `#007583`、次文字灰 `#525864`、警示
    Rose Crimson `#B91C1C`、背景 `#FDFCFA`。不要使用 Mermaid 預設配色。
3.  在 Gamma Prompt 輸出中，該 Slide 的大綱文字仍保留**一句自然語言描述**該頁圖表在
    講什麼（給 Gamma 排版文字用），但不要求 Gamma 自己畫出精確圖表。
4.  在最終輸出說明中，明確指示使用者：「請先用 Mermaid 渲染工具（如 mermaid.live）
    把上方這段圖表轉成圖片，再手動插入/替換 Gamma 生成的對應頁面」。
```
```

- [ ] **Step 2: Verify Module 6 has no leftover placeholder**

Run: `grep -n "Task 6 補上" "templates/_shared-modules.md"`
Expected: no match.

- [ ] **Step 3: Add the diagram-strategy stage to `1_to_n_slide_prompt_template.md`**

Insert a new `## 第四階段：流程圖策略` section directly **before** `## 輸出格式` (i.e. after the end of Task 5's updated `第三階段` section). Content: the full Module 6 markdown block from Step 1, prefixed with:

```markdown
## 第四階段：流程圖策略（Mermaid 先繪圖，再以圖片插入 Gamma）

<!-- SYNC: _shared-modules.md#module-6-mermaid-流程圖策略 -->
```
(then the same numbered 1-4 content and four Mermaid code blocks as Step 1).

- [ ] **Step 4: Update Slide 5 & 6 instructions inside `1_to_n_slide_prompt_template.md`'s Gamma-prompt output block**

Find:

```markdown
## Slide 5: [第五頁標題 - 使用者互動與流程]
*   互動流程流向（卡片連接關係）：[輸入源] ➔ [AI 核心處理] ➔ [用戶反饋/雙重驗證] ➔ [下游任務派發與同步]
*   互動步驟描述：
    *   步驟 1 [輸入端]：[用戶行為描述，嚴禁使用無結構文字]
    *   步驟 2 [AI 處理]：[系統行為描述]
    *   步驟 3 [校對與驗證]：[交互細節描述]
    *   步驟 4 [完成匯出]：[最終價值交付點描述]

## Slide 6: [第六頁標題 - 系統整合架構圖]
*   系統整合架構流向（圖形化卡片關係）：[既有主產品架構] ➔ [AI 核心運算層] ➔ [新功能交互介面]
*   系統模組結構描述：
    *   既有系統整合點：[描述與主產品系統的串接細節]
    *   原型介面佈局：[描述 UI 與前後台的串接，嚴禁使用無結構文字]
```

Replace with:

```markdown
## Slide 5: [第五頁標題 - 使用者互動與流程]
*   一句話描述本頁流程（給 Gamma 排版文字用）：[輸入源] ➔ [AI 核心處理] ➔ [用戶反饋/雙重驗證] ➔ [下游任務派發與同步]
*   對應的 Mermaid 圖表（見「第四階段：流程圖策略」的「橫向編號步驟卡」範本，套用本頁實際步驟文字）——**使用者需自行用 Mermaid 渲染工具轉成圖片後插入本頁**，不要求 Gamma 自己畫出精確圖表。
*   互動步驟描述（供 Mermaid 節點文字與演講稿使用）：
    *   步驟 1 [輸入端]：[用戶行為描述，嚴禁使用無結構文字]
    *   步驟 2 [AI 處理]：[系統行為描述]
    *   步驟 3 [校對與驗證]：[交互細節描述]
    *   步驟 4 [完成匯出]：[最終價值交付點描述]

## Slide 6: [第六頁標題 - 系統整合架構圖]
*   一句話描述本頁架構（給 Gamma 排版文字用）：[既有主產品架構] ➔ [AI 核心運算層] ➔ [新功能交互介面]
*   對應的 Mermaid 圖表（見「第四階段：流程圖策略」的「Z 字型技術管線圖」範本，套用本頁實際模組名稱）——**使用者需自行用 Mermaid 渲染工具轉成圖片後插入本頁**。
*   系統模組結構描述（供 Mermaid 節點文字與演講稿使用）：
    *   既有系統整合點：[描述與主產品系統的串接細節]
    *   原型介面佈局：[描述 UI 與前後台的串接，嚴禁使用無結構文字]
```

- [ ] **Step 5: Update Slide 4 instructions inside `0_to_1_slide_prompt_template.md`'s Gamma-prompt output block**

Find:

```markdown
## Slide 4: [第四頁標題 - 使用者互動與流程]
*   互動流程流向（卡片連接關係）：[用戶輸入] ➔ [AI 核心處理] ➔ [用戶反饋/雙重驗證] ➔ [匯出/分享產出]
*   互動步驟描述：
    *   步驟 1 [輸入端]：[用戶行為描述，嚴禁使用無結構文字]
    *   步驟 2 [AI 處理]：[系統行為描述]
    *   步驟 3 [校對與驗證]：[交互細節描述]
    *   步驟 4 [完成匯出]：[最終價值交付點描述]
```

Replace with:

```markdown
## Slide 4: [第四頁標題 - 使用者互動與流程]
*   一句話描述本頁流程（給 Gamma 排版文字用）：[用戶輸入] ➔ [AI 核心處理] ➔ [用戶反饋/雙重驗證] ➔ [匯出/分享產出]
*   對應的 Mermaid 圖表（見「第四階段：流程圖策略」的「橫向編號步驟卡」範本，套用本頁實際步驟文字）——**使用者需自行用 Mermaid 渲染工具轉成圖片後插入本頁**，不要求 Gamma 自己畫出精確圖表。
*   互動步驟描述（供 Mermaid 節點文字與演講稿使用）：
    *   步驟 1 [輸入端]：[用戶行為描述，嚴禁使用無結構文字]
    *   步驟 2 [AI 處理]：[系統行為描述]
    *   步驟 3 [校對與驗證]：[交互細節描述]
    *   步驟 4 [完成匯出]：[最終價值交付點描述]
```

- [ ] **Step 6: Add the diagram-strategy stage to `0_to_1_slide_prompt_template.md`**

Same as Step 3, insert `## 第四階段：流程圖策略（Mermaid 先繪圖，再以圖片插入 Gamma）` directly before its `## 輸出格式` heading.

- [ ] **Step 7: Verify no SVG/CSS diagram syntax remains and Mermaid is present**

Run: `grep -n "viewBox\|\.ct-grid\|\.figure" "templates/1_to_n_slide_prompt_template.md" "templates/0_to_1_slide_prompt_template.md"`
Expected: no match.

Run: `grep -c '```mermaid' "templates/1_to_n_slide_prompt_template.md" "templates/0_to_1_slide_prompt_template.md" "templates/_shared-modules.md"`
Expected: 4 in each of the two templates (one per diagram type), 4 in the shared module.

- [ ] **Step 8: Commit**

```bash
git add templates/_shared-modules.md templates/1_to_n_slide_prompt_template.md templates/0_to_1_slide_prompt_template.md
git commit -m "feat: replace SVG/CSS diagram directives with Mermaid diagram strategy

Gamma cannot reliably render inline SVG/CSS or guarantee it preserves
hand-built markdown layouts, so flowchart/architecture slides now get
a standalone Mermaid code block (styled to design-system-portfolio-site
tokens) that the user renders to an image and manually inserts, instead
of asking Gamma to draw the diagram itself."
```

---

## Task 7: Final consistency pass across all three files

**Files:**
- Modify (light touch only): `templates/1_to_n_slide_prompt_template.md`
- Modify (light touch only): `templates/0_to_1_slide_prompt_template.md`
- Read-only check: `templates/_shared-modules.md`

**Interfaces:**
- Consumes: everything produced by Tasks 1-6.
- Produces: a verified-consistent final state — no task after this one depends on further edits.

### Steps

- [ ] **Step 1: Confirm every `_shared-modules.md` module has a matching `<!-- SYNC -->` tag in both templates**

Run: `grep -n "SYNC: _shared-modules.md" "templates/1_to_n_slide_prompt_template.md"`
Expected: 8 lines, one per module anchor used by 1-to-N (module-1, module-2 1-to-N variant, module-3 ×3 (執行架構總覽 + 理論基礎 + 拆鷹架寫作原則), module-4, module-5, module-6).

Run: `grep -n "SYNC: _shared-modules.md" "templates/0_to_1_slide_prompt_template.md"`
Expected: 8 lines, same pattern for the 0-to-1 variant.

- [ ] **Step 2: Confirm no scaffold placeholders remain in `_shared-modules.md`**

Run: `grep -n "補上" "templates/_shared-modules.md"`
Expected: no match.

- [ ] **Step 3: Confirm the P1/P2/P3 phase-label warning from the design doc is present**

Run: `grep -n "P1.*P2.*P3" "templates/1_to_n_slide_prompt_template.md" "templates/_shared-modules.md"`
Expected: at least one match in each (added in Task 2, Step 1 and Step 3).

- [ ] **Step 4: Confirm the usage instructions at the top of each template still make sense given the new Slide 0**

Read the `> **使用方式：**` block at the top of `templates/1_to_n_slide_prompt_template.md` (lines 1-4) and `templates/0_to_1_slide_prompt_template.md` (lines 1-4). If either still says "**7 頁大綱**" / "**6 頁大綱**" without mentioning the cover slide, append one clause, e.g. for 1-to-N:

```markdown
> **使用方式：**
> 複製此模板的全部內容，並在最下方的 `<input_documents>` 中貼上你功能的 `spec.md` 與 `plan.md`，然後發送給 AI 助手。它將會產出一份**可以直接複製貼進 Gamma 簡報生成軟體的 Prompt（含封面頁、大綱與嚴格風格指令）**，以及每一頁的演講講稿。
```

(replace the word "含大綱" with "含封面頁、大綱" in both files' usage blocks — apply the equivalent one-word insertion to 0-to-1's usage block too).

- [ ] **Step 5: Run the full regression grep sweep**

```bash
grep -rn "5 隻虛擬 Agent 共識會議\|48B7BD\|viewBox\|大盤 NSM\|大盤北極星指標\|大盤問題陳述" templates/1_to_n_slide_prompt_template.md templates/0_to_1_slide_prompt_template.md
```
Expected: no output (empty, exit code 1) — confirms every superseded mechanism/color/syntax from the design doc's Section 4 ("明確不採用的方向") and Section 3 fixes is fully gone.

**Known, expected exception (do not "fix" this):** `templates/1_to_n_slide_prompt_template.md:30` legitimately contains the literal string `大盤指標` inside the pre-existing audit rule that *names* the banned phrase (`"一律禁止使用「大盤指標」等不專業敘述，統一使用「產品北極星指標」"`) — this is the rule definition itself, analogous to how the Output Register Guardrail's own text names `自嗨`/`虛胖` as forbidden words. Do not grep for the bare substring `大盤指標` in this sweep (it would false-positive on that legitimate line) — the more targeted patterns above (`大盤 NSM`, `大盤北極星指標`, `大盤問題陳述`) catch the informal-usage instances without matching the rule-definition line. `0_to_1_slide_prompt_template.md:63` and `104` and `_shared-modules.md:50` also legitimately retain generic descriptive uses of "大盤" (meaning "aggregate/overall," e.g. "大盤與子功能之分") that are not the banned metric-naming pattern and are out of scope for this plan — leave them.

- [ ] **Step 6: Commit**

```bash
git add templates/1_to_n_slide_prompt_template.md templates/0_to_1_slide_prompt_template.md
git commit -m "docs: update usage instructions to mention the new cover slide

Final consistency pass confirming all SYNC anchors match
_shared-modules.md and no superseded mechanisms/colors/syntax remain."
```

---

## Self-Review Notes (completed while writing this plan)

1. **Spec coverage**: §3.A → Task 2. §3.B → Task 3. §3.C → Task 4. §3.D → Task 6. §3.E → Task 5. §3.F → Tasks 1-6 (SYNC tags) verified in Task 7. §3.G → Task 3 Step 4/5. §3.H (added mid-execution, after Task 1 shipped) → Task 3 Steps 1/4/5/6/7. §4 ("不採用的方向") → verified negatively in Task 7 Step 5. All design-doc sections have a task.

**Post-Task-1 amendment record**: after Task 1 shipped and its reviewer flagged a Module-1-vs-template wording drift (fixed directly via commit `a530a0a`, not re-running Task 1), the user added a new requirement — the pptx's Slide 3 "拆鷹架/REMOVE SCAFFOLDING NOISE" principle — which was folded into Task 3 (not yet started at the time) as new Steps 6/7 and an amended Step 1/4/5/8/9/10, rather than requiring a whole new task. This plan file reflects that amendment; no separate "Task 3.5" exists.
2. **Placeholder scan**: the only placeholder-looking text is the `（Task N 補上）` scaffold markers in Task 1's Step 1, which are explicitly filled in by Tasks 2-6's Step 1 — by the end of Task 6 none remain (verified in Task 7 Step 2). No other TBD/TODO patterns were introduced.
3. **Type/name consistency**: `<!-- SYNC: _shared-modules.md#module-N-... -->` anchor slugs are used identically wherever referenced (Task 7 Step 1 greps for the literal substring, not the full slug, so slug-casing drift won't silently pass — if a slug is misspelled in one file it will still count toward the grep total but Task 7 Step 1's "6 lines" expectation forces a manual look at the actual anchors, catching drift). Color hex values (`#153166`, `#007583`, `#525864`, `#B91C1C`, `#FDFCFA`) are copy-pasted identically across Tasks 4, 5, 6 rather than re-derived, avoiding transcription drift.
