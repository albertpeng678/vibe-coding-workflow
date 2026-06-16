# Vibe Coding Cookbook — 給初心者的 0→1 實務流程

一份寫給 **vibe coding 初心者** 的操作手冊（cookbook）：說明如何用 AI coding agent，搭配 **superpowers / Karpathy 工作紀律**與一套 skill / tool / MCP，把一個念頭從 **0 做到上線維運**。

全文以「**法規 RAG 問答 agent**」為貫穿範例——但**範例只是配角，方法論才是主體**。你學的是一套可套用到任何產品的流程。

## 這份文件在解決什麼

初學者談 vibe coding 多半停在「叫 AI 寫個小東西」。這份 cookbook 帶你走完**真實產品都會經歷的七個環節**，每一步都明確告訴你：用哪個工具、貼哪段提示詞、怎麼確認你做對了，並大量使用 mermaid 流程圖降低理解成本。

## 結構（Part 0–4）

| 部分 | 內容 |
|---|---|
| Part 0 | 如何使用本文件（地圖、慣例、成品預覽） |
| Part 1 | 你的工具箱（逐一說明每個 skill / tool / MCP + 安裝方式） |
| Part 2 | 心法（你是建築師，不是旁觀者） |
| Part 3 | 主線：0→1 七個環節（需求釐清 → 規格 → 實作計劃 → 開發 → 測試 → 部署 → 上線後維運） |
| Part 4 | 附錄（Prompt 速查、對照表、自行打造 design.md…） |

## 檔案

- `vibe-coding-cookbook.md` — cookbook 主檔（撰寫中）
- `docs/superpowers/specs/` — 設計規格（spec）
- `assets/` — 文件內嵌圖片

## 交付形式

單一 Markdown 主檔，另輸出 **PDF / Word**；因轉檔常跑版，交付前以 **playwright-cli + Playwright MCP** 做視覺驗收。

## 視覺與慣例

- 對齊 **Airy Glass** design system：navy 主色 + teal 強調、主色 ≤5、Lucide icon（**禁 emoji**）。
- 統一 recipe 骨架、為掃描而寫、地圖優先。

## 進度

- 已完成：Part 0、Part 1、Part 2；Part 3 環節 1（需求釐清）、環節 2（規格確認）。
- 進行中：Part 3 環節 3（實作計劃）起。
