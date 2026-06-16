# CLAUDE.md — vibe-coding-workflow 專案導覽

> 這份檔案會被 Claude Code 自動讀取。動工前請先讀一遍，建立全貌。

## 這是什麼

正在製作一份「**給 vibe coding 初心者的 0→1 cookbook**」。

- 主檔：`vibe-coding-cookbook.md`
- 設計規格（**先讀這個了解全貌**）：`docs/superpowers/specs/2026-06-16-vibe-coding-cookbook-design.md`

## 核心定位

- **vibe coding 方法論為主體**；「法規 RAG 問答 agent」只是貫穿全文的**配角範例**，任何時候方法論優先。
- TA 是初心者：資訊要易理解，但不失豐富度。

## 製作方式

- **一個環節一個環節做，每節先與使用者討論再寫**（brainstorming 式協作）。
- 全文完成後 → 套 Airy Glass 樣式渲染 HTML → 匯出 PDF / Word → 用 **playwright-cli + Playwright MCP 做視覺驗收**（檢查 mermaid、有無跑版）。

## 全文必守慣例

- **Icon**：禁用 emoji。一律用 Lucide，原始檔以 `{{icon:名稱}}` 語法標記（渲染時換 SVG）。常用：`clipboard`(複製提示詞)、`circle-check`(預期結果)、`triangle-alert`(注意)、`lightbulb`(深入理解)、`wrench`(疑難排解)、`arrow-right`(下一步)。
- **視覺**：對齊 `QA-assistant/design-system.md`（Airy Glass）——navy 主色 + teal 強調、主色 ≤5、oklch。
- **佔位符**：`<全大寫_底線>`，務必包在 code block 內。
- **提示詞**：繁體中文、可直接複製貼上；附填空指引與填好的範例。
- **寫作**：一段一重點、倒金字塔、粗體標關鍵字、清單化、描述性小標（layer-cake）、地圖優先（每章開頭一張 mermaid）。

## 結構

Part 0 如何使用 → Part 1 工具箱 → Part 2 心法 → Part 3 七環節（需求釐清／規格確認／實作計劃／正式開發／測試／部署上線／上線後維運）→ Part 4 附錄。

每個環節用統一 recipe 骨架：`成果一句話 → 前置需求 → 流程概覽圖 → 步驟(內嵌可複製 prompt) → 完成檢查 → 疑難排解 → 下一步`。

## 注意

- `QA-assistant/` 是**參考用的 clone 範例 repo**（已 gitignore），不是本專案的一部分，不要修改或當成主線內容。
