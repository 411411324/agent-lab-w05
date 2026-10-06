# My lab evidence / 我的實作紀錄

Use a group code, not real names or student IDs in shared files. / 共用檔只寫組別代碼，不寫姓名或學號。

- Group code / 組別：W05-01
- Tool / 工具：Antigravity
- Route / 路線：individual 個人
- Tasks completed / 完成題目：A, B, C, D
- Material / 素材：NDHU classroom tasks 東華課堂版
- For original-pack work: task number, author/source link and version / 原版實作：題號、作者來源連結與版本：無（使用東華課堂版）
- My role and what I checked / 我的角色與實際檢查：負責提示詞下達、操作計畫審核、檔案 SHA-256 雜湊比對與原檔保護驗證、網頁端互動功能與極端條件測試、資料清洗邊界條件檢查、審核退回不安全計畫。

## Scope and plan / 範圍與計畫

Allowed input and output folders / 可讀取與輸出的資料夾：
- Task A：input 為 `practice/01-club-files/input`，output 為 `practice/01-club-files/output`
- Task B：input 為 `practice/02-campus-picker/activities.json`，output 為 `practice/02-campus-picker/output`
- Task C：input 為 `practice/03-equipment/equipment.json`，output 為 `practice/03-equipment/output`
- Task D：input 為 `practice/04-review/bad-plan.txt`，output 為 `practice/04-review/my-rejection.md`

What I asked for / 原始需求：
- **A 題**：盤點 12 個文字檔，原檔完全不動，提出整理分類計畫；經確認後複製至適當子目錄，保留重複與不同版本，產出 `report.md` 與 12 筆物件之 `manifest.json`。
- **B 題**：根據 `activities.json` 製作純離線單頁「課間我想做什麼？」活動挑選器，具備地點/時間/強度篩選、隨機挑選、最近5次歷史紀錄、重設篩選、中英雙語即時切換。
- **C 題**：清理 `equipment.json`，修剪前後空白（qty不修剪），統一借用狀態（available/borrowed/unknown），移除全空物件，原樣保留缺漏或負數數量，保留相同 ID 之紀錄與衝突報告，產出 `normalized.json` 與 `issues.md`。
- **D 題**：審核刻意寫錯的 `bad-plan.txt`，指出違規操作，提出安全合規之替代修正方案。

What I checked before execution / 動手前我檢查了什麼：
- 檢查工具權限與作業目錄邊界，確認僅存取專案內指定題目資料夾，不碰 Downloads 或外部檔案。
- 檢查原檔保護承諾：確認 Agent 在第一階段僅唯讀分析並提出計畫，未獲「執行」回覆前絕不動檔案。
- 檢查檔案數量與內容：確認 input 檔數為 12，發現完全重複檔（如 `announcement` 與 `announcement_copy`），以及檔名相近但內容不同且未定案之版本（`proposal_final.txt` 與 `proposal_final2.txt`）。

## Tests actually performed / 我真的做過的測試

| Test / 測試 | Expected / 預期 | Observed / 實際 | Evidence / 證據 |
|---|---|---|---|
| 1. B 條件精確篩選（室內/15分/低強度） | 只可能選出 A01、A02、A03、A04 之一 | 抽取結果為 A02（畫一張小卡，15 分鐘，室內，低強度），符合全部篩選條件 | `practice/02-campus-picker/output/index.html` 畫面顯示 A02，歷史紀錄新增該筆 |
| 2. B 無符合條件測試（室外/15分/中強度） | 顯示「沒有符合條件的活動」，不放寬條件且不記錄至歷史清單 | 畫面以紅底警示顯示「沒有符合條件的活動」，歷史紀錄未增加無效抽取 | `practice/02-campus-picker/output/index.html` 之 `currentPicked === 'none'` 渲染 |
| 3. A 檔案完整性與雜湊檢驗 | 12 個輸出檔案與輸入原檔之 SHA-256 雜湊值 100% 一致，原檔無變更 | 執行 SHA256 腳本檢驗 12 筆對應檔案，全部顯示 MATCH，原檔修改時間與大小未變 | `practice/01-club-files/output/manifest.json` 與 `report.md` |
| 4. C 器材資料清洗檢驗 | 10 列轉為 9 列有效，第 6 列全空列移除，EQ01/EQ02 均保留，異常數值原樣保留 | normalized.json 恰為 9 筆有效物件，source_row 7 為 `""`，source_row 8 為 `-1`，source_row 9 為 `unknown` | `practice/03-equipment/output/issues.md` 與 `normalized.json` |

## One revision / 一次修改

Before / 原來的情況：
B 題第一版（v1）在點擊「幫我選」按鈕前，使用者無法得知當前條件下有幾筆符合的活動；此外只能用滑鼠點擊按鈕，操作便利性與無障礙程度較低。

Request / 我提出的修改：
新增即時符合數量提示標籤（例如中：「目前符合條件：4 項活動」/ 英：「Matching activities: 4」，若 0 筆則紅底醒目標示），並新增鍵盤快捷鍵支援（Enter / Space 鍵快速抽取活動、Esc 鍵重設篩選），且完美適配中英雙語切換。

After and retest / 修改後與重測結果：
修改後（v2）切換至「室外／15分鐘／中強度」時，標籤即時更新為「目前符合條件：0 項活動」；在頁面上直接按下鍵盤 Enter 鍵即可成功抽取活動，按下 Esc 鍵篩選即刻重設為預設值，標籤也即時恢復為 12 項。

New requirement or defect? / 新需求還是原規格未做到？
新需求（v1 已完整符合原始規格之單頁離線隨機挑選與篩選，即時數量提示與快捷鍵支援為進一步的使用者體驗增強）。

## One rejection / 一次退回

Which action I reject and why / 退回哪個動作、為什麼：
退回 `bad-plan.txt` 中「整理整個 Downloads 資料夾」、「刪除重複檔」、「把 final2 當最新版」、「找不到資料補合理值」以及「自動公開成果」。因為其擅自擴大目錄範圍至使用者私人 Downloads、執行破壞性刪檔、憑檔名主觀臆測定稿、擅自偽造數據，且未經授權即對外公開發佈，嚴重違反資料完整性與資安規範。

An acceptable alternative / 可以怎麼改：
作業範圍嚴格限制於指定子資料夾內；原始檔案一律保留不更動；重複與相近版本均留副本並於報告中列出待人工裁定；缺漏值原樣保留或標記 unknown 並回報問題；成果僅存放於本機 output 目錄，待人工驗收核准後方可決定是否發佈。詳見 `practice/04-review/my-rejection.md`。

## Still unverified / 還沒驗證

What I cannot claim is complete / 哪些事不能說已完成：
1. **Task A 企畫定案與預算決策**：`proposal_final.txt`（室外30分）與 `proposal_final2.txt`（室內20分）兩者何為最終定案方案，以及紙張預算 100 是否獲准，仍待幹部會議與總務實體審查核定。
2. **Task B 隨機機率分佈**：挑選器雖已完整通過各條件組合與極端測試，但有限次數的手動抽樣無法從數學上證明偽隨機分佈完全公平；且活動內容為教學模擬，非校方真實活動。
3. **Task C 實體庫存確認**：`EQ02` 數量衝突（2 還是 3）以及 `EQ05` 負數（-1）、`EQ04` 缺數量，均為數據品質問題，必須待管理人員實際盤點實物後方可確認正確庫存。
