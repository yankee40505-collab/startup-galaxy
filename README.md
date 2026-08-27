# 創業星系

Ray 手上正在轉的專案，用一張互動星圖呈現。

點任一顆星球會進入該專案的「宇宙」頁，顯示簡介、關鍵欄位與底下的四顆衛星。按 `←` 返回星系或 `Esc` 關閉。

## 現在有兩份

| 版本 | 用途 |
|---|---|
| **Claude Artifact**（主力） | 可以直接在頁面上編輯四顆衛星的清單，按「儲存」就存進去，換裝置也看得到 |
| 這個 repo | 程式碼備份與唯讀展示。**內容凍結在 2026-08-27**，之後 Artifact 上的修改不會同步回來 |

Artifact 網址在 Ray 的 Claude 帳號裡（claude.ai/code/artifacts）。

## 星球

| 軌道 | 專案 |
|---|---|
| 01 | GRV ENGLISH |
| 02 | Ray's English Corner |
| 03 | 大懶豹國際娛樂 |
| 04 | 大懶豹小劇場 |
| 05 | Knowledge Tycoon |
| 06 | 紐西蘭打工度假 2027 |

星球的大小代表投入程度，離中心的距離代表離日常的遠近。星球右上角的數字是還沒完成的待辦數。

## 檔案

- `artifact.html` — 原始檔（body 片段，發佈到 Artifact 用的就是這個）
- `index.html` — 由 `artifact.html` 組出來的完整 HTML，給 GitHub Pages 用

兩個檔案的 CSS、版型、程式碼完全一樣，差別只在外層有沒有 `<html><head>`。

## 要改內容

**四顆衛星的清單（待辦／定期／未來／收益）** 在 Artifact 上直接編輯就好，不用動程式碼。

其餘的東西還是改 `artifact.html`：

- `PLANETS` 陣列（在 `<script id="app">` 裡）
  - `r` — 離中心的距離（百分比）
  - `size` — 直徑（佔星圖寬度的百分比）
  - `angle` / `speed` — 起始角度與公轉速度
  - `lede` / `meta` — 宇宙頁的簡介與關鍵欄位
  - `satNote` — 某顆衛星上方的補充說明
  - `schedule` — 發文排程（目前只有 GRV 有）
- `<script id="state">` — 四顆衛星的初始清單。Artifact 每次儲存都會覆寫這一段。

## 它怎麼存檔的

頁面拿到 `artifact` 能力後，把整份文件重新組出來再發佈一次新版本：CSS、靜態 HTML、程式碼三段都是從 DOM 裡原封不動讀出來的，只有 `<script id="state">` 那段 JSON 會換掉。所以存幾次都不會走鐘——同樣的內容存兩次，產出的檔案是逐位元組相同的。

沒有 `artifact` 能力的地方（GitHub Pages、直接開檔案）不會出現編輯按鈕，就是一個唯讀網站。
