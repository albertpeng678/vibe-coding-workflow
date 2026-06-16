# Vibe Coding Cookbook — 設計規格（Spec）

> 日期：2026-06-16　｜　狀態：設計鎖定中，逐環節製作前的藍圖
> 一句話：給 **vibe coding 初心者** 的 0→1 實務流程 cookbook，以「法規 RAG 問答 agent」為**貫穿範例**，教讀者用 superpowers / karpathy 工作紀律 + 一套 skill/tool，把點子做到上線維運。

---

## 1. 目標與定位

- **主體**：vibe coding 的**方法論與實務流程**（產品無關的通用 0→1 生命週期）。
- **範例**：法規 RAG 問答 agent（OpenAI file search 為檢索核心）**只是配角**，用來具體示範每個環節。任何時候「方法論 > 範例技術細節」。
- **TA**：vibe coding 初心者。需從他們角度確保「資訊易理解」，同時「不失資訊豐富度」。
- **核心主張**（靈魂）：vibe coding 不是「放手不審查」。Karpathy 原意僅適用丟棄式週末專案；要上線的產品需要更有紀律的 **Agentic Engineering**。讀者是**建築師，不是旁觀者**。初學者最大風險是分不出 AI 產出中「看似合理的錯誤」。

## 2. 交付物（Deliverables）

1. **單一 Markdown 主檔**（`vibe-coding-cookbook.md`）：含全部章節與 mermaid。
2. **PDF 匯出**。
3. **Word（docx）匯出**。
4. **視覺驗收**：PDF/Word 轉檔常跑版，交付前**用 playwright-cli skill 操作 Playwright MCP** 渲染後截圖檢查（mermaid 是否正常、有無溢出/破版/斷行錯誤），通過才算完成。

## 3. 視覺設計（對齊既有「Airy Glass」design system）

- **唯一視覺真相**：對齊 repo 的 `design-system.md`（Airy Glass）。
- **色彩**：navy `--primary` 為主、teal `--brand-accent` 為唯一品牌強調、中性灰階；功能色 success / warning / destructive。**主色 ≤ 5**。oklch。亮/暗模式（文件預設亮色）。
- **Icon**：**全面禁用 emoji**。一律取自 **Lucide**（單一 icon library），統一線寬與尺寸。
- **排版人格**：translucent / rounded / airy；慷慨留白、CJK 欄寬 ≤40 字、body 行高 1.5。
- **渲染管線**：Markdown →（套 Airy Glass token 的）HTML → PDF / docx。

## 4. 全書統一慣例（Conventions）

### 4.1 Recipe 骨架（每個環節都用）
```
## 環節名稱（動詞 + 成果）
> 你會得到什麼（一句話成果）｜預估時間｜難度
### 你需要先有（Prerequisites）— checklist
### 流程概覽 — mermaid
### 步驟 — 祈使動詞；內嵌可複製 prompt + 填空指引 + 預期結果
### 完成檢查（Checkpoint）— checklist
### 疑難排解 — 表格（症狀 | 可能原因 | 怎麼辦）
### 下一步 — 連到下一環節
```

### 4.2 Callout icon（Lucide，無 emoji）
| 用途 | Lucide icon | 語意色 |
|---|---|---|
| 複製提示詞 | `clipboard` | primary |
| 預期結果 | `circle-check` | success |
| 注意 / 踩坑 | `triangle-alert` | warning |
| 深入理解 | `lightbulb` | brand-accent |
| 疑難排解 | `wrench` | muted |
| 下一步 | `arrow-right` | primary |

### 4.3 提示詞與佔位符
- 提示詞以**繁體中文**撰寫，獨立 code block、可一鍵複製，前綴一行「用途」。
- 佔位符：`<全大寫_底線>`（例：`<你的產品一句話描述>`），務必包在 code block 內；下方附「填空指引」與一個填好的真實範例。

### 4.4 寫作原則（NNgroup 實證）
- 一段一重點、倒金字塔、粗體標關鍵字、清單化、描述性小標（layer-cake）、字數砍半、客觀語氣。
- 漸進揭露：主線只給「最短可行路徑」；原理 / 進階 / 捷徑收進可選層（≤2 層）。
- 地圖優先：每章開頭一張總覽 mermaid，讓讀者知道「我在哪、接下來去哪」。
- 圖：初學場景 90% 用 flowchart（步驟+決策）與 sequence（工具互動）；每張 ≤15 節點、圖前一句導言、圖負責結構/文字負責細節。

## 5. 結構骨架

```
Part 0 · 如何使用本書        本書地圖(全景 mermaid) + 慣例說明 + 成品預覽
Part 1 · 你的工具箱          以「解決什麼問題」說明每個 skill/MCP + 環節對應總表
Part 2 · 心法                vibe coding 是建築師心態（Karpathy 四原則 + 看似合理的錯誤）
Part 3 · 主線：0→1 七個環節   每環節一個 recipe 骨架
Part 4 · 附錄                Prompt 速查 / skill·tool 對照 / 常見錯誤 / 詞彙表 / 自行打造你的 design.md /（深入理解）
```

- 不加 15 分鐘 Quickstart（已確認）。
- 提案收尾（proposal-template → Gamma）：接近完成時再決定是否納入。

## 6. Part 1「你的工具箱」內容（problem-first）

進主線前，先用「解決什麼問題」的角度逐一說明，並附「環節 ↔ skill/tool」總覽表。

- **superpowers / using-superpowers**：解決「AI 隨意發揮、缺乏工作紀律」。
- **brainstorming**：解決「需求沒釐清就動工，做錯方向」。
- **writing-plans**：解決「規格與計畫含糊，開發失焦」。
- **TDD / test-driven-development**：解決「不知道何謂完成、改壞沒人知道」。
- **systematic-debugging**：解決「卡 bug 亂試、沒有方法」。
- **dispatching-parallel-agents**：解決「研究/開發序列化太慢、覆蓋不足」。
- **frontend-design + visual companion**：解決「UI 醜、像 AI 生成的通用樣板」。
- **karpathy-guidelines**：解決「過度設計、改動失控、假設沒講清楚」。
- **playwright-cli / playwright-core**：解決「不知道做出來的東西到底能不能跑」。
- **Context7 MCP**：解決「LLM 知識過時、幻覺出不存在/已棄用的 API」。
- **Web Search（NNgroup + 近似產品分析）**：解決「閉門造車，不了解使用者與市場」。
- **Playwright MCP**：解決「需要真的開瀏覽器點點看、重現問題」。
- **Railway（CLI + GitHub-CICD）**：解決「部署/DB/環境變數對新手太難」。
- **Sentry（MCP + Seer）**：解決「上線後出錯不知道、無法根因分析」。

## 7. 主線七環節 ↔ skill/tool 對應（定稿）

| 環節 | 主要 skill / tool | 範例(RAG agent)示範什麼 |
|---|---|---|
| **1·需求釐清**（需求細節+視覺） | brainstorming、visual companion、frontend-design、**dispatching-parallel-agents**、Web Search（NNgroup UI/UX ＋**國內外近似產品分析**）、**Context7（探查技術社群對此需求的解法）** | 釐清要做什麼、出前端 mockup、查近似產品與可行技術 |
| **2·規格確認** | writing-plans | 把需求落成 spec.md（**不**用 Context7） |
| **3·實作計劃** | writing-plans、**Context7（搜技術社群主流解法、確保方案具效度）**、**dispatching-parallel-agents** | 像 TPM 把規格落為開發計畫 plan.md；驗證解法效度 |
| **4·正式開發** | TDD、Context7、systematic-debugging、karpathy-guidelines、code review、**dispatching-parallel-agents（並行提升開發效率）** | file search 核心、chunking、前端、Postgres 都在此示範 |
| **5·測試** | playwright-cli、playwright-core、Playwright MCP | 問答流程 E2E |
| **6·部署上線** | Railway（CLI + GitHub-CICD） | **先建 GitHub repo → 推上去 → 拿到 repo 網址 → Railway 以該 repo 部署**；CLI 開 Postgres、設 variables、看 logs |
| **7·上線後驗證維運** | Sentry（MCP + Seer）、**playwright-cli、playwright-core、Playwright MCP（重現問題最關鍵）** | 抓生產錯誤、重現、根因分析、修 bug |

## 8. 範例產品定義（配角，固定設定）

- 產品：法規 RAG 問答 agent。
- 檢索核心：OpenAI file search（託管 vector store，**不自建 RAG**）。
- 應用資料層：**Railway Postgres**，存「問答歷史記錄」+「回答回饋/評分」。
- 無帳號登入（單一共用實例）。
- 技術棧：Python / FastAPI / openai SDK / pytest。
- 部署：Railway，GitHub 連結式 CICD（禁 `railway up` 本地直推）；CLI 負責 Postgres 開通、variables、logs。

## 9. 研究依據（已完成 5 路並行調研）

1. NNgroup 易讀性：scannability / progressive disclosure / information scent / cognitive load / 視覺輔助 / 新手 vs 專家。
2. 技術 cookbook 結構：Diátaxis 四象限、recipe 骨架、佔位符慣例、薄概念厚步驟。
3. Vibe coding 與 Karpathy：定義澄清、四原則、初學者陷阱與預防。
4. Mermaid：圖型選擇、易讀性、反模式、範例。
5. 工具鏈：Context7 / Playwright(MCP·CLI) / Railway CLI / Sentry 的角色與指令。

## 10. 製作方式

- **逐環節協作**：一個 Part / 環節討論並產出，最後組合成完整 cookbook。
- 每章遵循 §4 慣例與 §3 視覺。
- 全部章節完成後 → 套 Airy Glass 樣式渲染 HTML → 匯出 PDF/Word → Playwright 視覺驗收。

## 11. 待決事項（Open）

- 提案收尾（proposal-template → Gamma）是否納入：接近完成時再問。
- PDF/Word 的實際轉檔工具鏈（如 pandoc / 瀏覽器列印）於進入渲染階段再定。
