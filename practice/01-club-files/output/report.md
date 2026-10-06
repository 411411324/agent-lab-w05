# 社團檔案整理報告 (Club Files Organization Report)

## 1. 整理概述
- **來源資料夾**：`practice/01-club-files/input`
- **目的資料夾**：`practice/01-club-files/output`
- **處理檔案總數**：12 個檔案（全數建立副本並分類，原始檔案未受任何更動）

---

## 2. 分類與對照架構

本整理將 12 個檔案依功能分為四個主要目錄：

### 2.1 企畫與活動方案 (`proposals/`)
- `proposal_final.txt`：企畫第一版草案（室外活動 30 分鐘草案）。
- `proposal_final2.txt`：企畫第二版草案（室內活動 20 分鐘待討論）。
- `rain_plan.txt`：雨天備案規劃（提及若下雨則另議室內方案）。
- `next_steps.txt`：後續待辦與比對指示（明確標明比較兩個企畫，兩者皆未定案）。

### 2.2 宣傳文案與公告 (`publicity/`)
- `announcement.txt`：活動準備通知（請帶筆記本，時間地點待定）。
- `announcement_copy.txt`：活動通知副本（內容與 `announcement.txt` 完全相同，保留副本）。
- `poster_text.txt`：文宣與宣傳標語（「一起來做一張小卡」）。

### 2.3 會議記錄與行政庶務 (`meetings_and_admin/`)
- `meeting_notes.txt`：會議決策摘要（下次討論室內或室外方案）。
- `budget_draft.txt`：預算草案（紙張預算模擬 100，尚未核定）。
- `feedback_questions.txt`：回饋問卷設計題目。

### 2.4 器材管理 (`equipment/`)
- `equipment_list.txt`：活動所需器材清單（markers: 4, paper packs: 2）。
- `equipment_backup.txt`：器材備份清單（內容與 `equipment_list.txt` 完全相同，保留副本）。

---

## 3. 疑似重複與版本差異分析

### 3.1 內容完全相同項目 (Identical Content)
1. **`announcement.txt` 與 `announcement_copy.txt`**
   - SHA-256：`c19164b1054ebf52ed33bc5321c887985ea043a0b07db1e99f866986d2ccd584`
   - 處理：兩份皆複製至 `output/publicity/` 保留，未做刪除或合併。
2. **`equipment_list.txt` 與 `equipment_backup.txt`**
   - SHA-256：`c21d53ba1f8d3ad06e1833539935120a5baca4d13b34a2aa98ce157ff4502fa3`
   - 處理：兩份皆複製至 `output/equipment/` 保留，未做刪除或合併。

### 3.2 檔名相近但內容完全不同版本 (Different Content)
- **`proposal_final.txt` vs `proposal_final2.txt`**
  - `proposal_final.txt`：提議「室外活動 30 分鐘草案」。
  - `proposal_final2.txt`：提議「室內活動 20 分鐘待討論」。
  - 判定原則：嚴禁透過字眼（如 `final` 或 `final2`）或檔案修改時間妄斷哪一份是「定稿」；依據 `next_steps.txt` 紀錄，兩者皆為提案階段，需待幹部會議決策。

---

## 4. 待確認問題 (Open Questions for Human Review)
1. **企畫定案決策**：室外（30分鐘）與室內（20分鐘）方案尚未由社團幹部投票定案，需會議確認。
2. **預算審核**：`budget_draft.txt` 標明模擬 100 尚未核定，需總務或社長審核通過。
3. **活動時間地點**：`announcement.txt` 提及「時間地點尚未決定」，後續發佈正式通知前須補齊資訊。
4. **重複檔去留**：`announcement_copy.txt` 與 `equipment_backup.txt` 屬完全重複檔，後續若需清理需經負責人同意。

---

## 5. 實際執行的檢查與驗證
- [x] **原始檔案完整性**：比對 `input/` 12 個檔案的 SHA-256 與 `output/` 中對應檔案的 SHA-256，雜湊值 100% 一致，原檔無任何更動。
- [x] **副本數量驗證**：`output/` 下各分類中對應的副本檔案總數恰好為 12 個。
- [x] **格式清單**：`manifest.json` 包含 12 筆物件，每筆均有 `source`、`destination`、`reason`。

### 還沒確認的部分
- 未經人工核定的企畫方案最終選案與預算審核。
- 實際活動的時間地點何時能填入公告中。
