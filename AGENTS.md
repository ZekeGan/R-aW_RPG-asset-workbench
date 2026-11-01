# AGENTS — 目前有效規則

本檔只放現行規則。2026-10-25 以前逐段累積的授權與驗證流水帳已原文存於 [docs/development/AGENTS_HISTORY.md](docs/development/AGENTS_HISTORY.md)，那是歷史，不是新指令來源。使用者最新明確決策永遠優先。

## 目前狀態

- 程式版號 0.5.11，正在準備發行，尚未發布 1.0.0。各版摘要見 [CHANGELOG](docs/CHANGELOG.md)。
- 0.5.4 `pack:zip` 的 ZIP、四語文件、12 份授權檔、版號及 SHA-256 已核對；0.5.5 補上確認掃描時的作業提示（typecheck、build、隔離 Electron 驗收通過）。
- 乾淨 Windows／舊資料升級驗收與 LGPL 發行義務核對仍待完成，見 [發行準備](docs/development/RELEASE_PREPARATION.md)。
- 使用者曾口頭回報手動測試「沒什麼大問題」，那是摘要回報，不補造逐項證據。
- 已推送到 origin/main，尚未發布；原生模組應保持 Electron ABI。

## 授權範圍

- 使用者已授權以完成 MVP 與發行準備為目標持續實作，包含 0.5 的四語介面、R-aW 品牌、專案管理、批量配對、掃描作業提示等已定案項目。
- **不自動**推送、打標籤、發布、改依賴或操作真實遊戲；保留所有本機修改，不格式化來源。提交規則見下方升版規則。
- OPEN-005（刪專案入口）已確認放在首頁「開啟專案」旁；其他未決項見 [OPEN_ITEMS](docs/handoff-2026-10-23/OPEN_ITEMS.md)，不擅自定案。

## 升版與提交規則（使用者 2026-11-01 指定）

- **每次修改完成後都升版並 commit**，包含只改文件的批次。一個完成並驗證的修改批次為一單位，不是每次存檔；不逐檔零碎提交。
- 一般修正與文件批次遞增 patch，功能里程碑另定 minor，1.0.0 須使用者明確確認發行階段。下一個版號為 0.5.12。
- 同步 `package.json`、`package-lock.json`（根專案兩處）、README 與 INDEX 的版號、新增 `docs/UPDATE_<版號>.md`（打包腳本依此檔名取更新紀錄，不可改名）及 `docs/CHANGELOG.md` 一行。
- commit 訊息簡述內容並含版號；只 commit，**不推送、不打標籤、不發布**，那些仍須使用者明確指示。

## 不變的產品規則

- 固定原圖不可覆寫；選用（active）與部署（deployed）分離，匯入不寫遊戲；外部變更阻擋套用與還原。
- 永久刪除專案只清理工具管理資料，須確認失去備份／還原能力，遊戲保持當前狀態。已部署版本與原圖不可單獨刪除。
- 視覺與版面以 Mockup 為準、Wireframe 為參考；Mockup 示意文字不得放寬靜態 PNG、基準保護等安全規則。
- 原 FR／SCREEN／DEC 編號與 H-B／H-D 追蹤號保留，不重編；`INTEGRATION_MANIFEST.json` 為當時交付紀錄不改寫；歷史交接包的內容未經使用者同意不改，2026-11-01 使用者已同意刪除其中與正本逐 byte 相同的副本（見 `docs/handoff-2026-10-23/reference/README.md`）。

## 驗證規則

- 沿用 npm。流程：`npm run typecheck`、`npm test`（Node ABI，先 `npm run native:node`）、`npm run build`；啟動 Electron 前 `npm run native:electron`。
- 報告真實執行結果；Windows 或真實遊戲未測不得標 PASS，歷史 PASS 不能代替本次結果。局部修改只驗證受影響部分，通過且無新變更時不重跑。

## 效率準則

- 在不影響品質的前提下節省 token：只讀相關段落，不重讀未變動內容，不重複輸出。
- 每次代碼開發結束後簡短回顧步驟，最多 1–3 項具體優化；回顧不得額外掃描專案或重跑測試。

## 接手入口

先讀 [docs/development/INDEX.md](docs/development/INDEX.md)；使用者文件為根目錄 [README](README.md)（預設英文，其他語言在 docs/user）。
