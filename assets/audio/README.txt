發音音檔系統（2026-08 改版）
================================

現在的做法：所有發音音檔用 edge-tts（微軟神經網路語音，en-US-JennyNeural，
語速 -8%）批次產生，再用 ffmpeg 做音量標準化＋去頭尾靜音，格式統一為
mp3 / 單聲道 / 44.1kHz / 128kbps。

檔名 = 該英文字/句子內容的 sha256 前 12 碼（例如 mooncake → 84d3eb5c1e5b.mp3）。
好處：同一個字在不同頁面只會有一個檔、換教材順序也不會對不上。

manifest.json  ── 「文字 → 檔名」對照表（給人看 / 之後寫工具用）
manifest.js    ── 網頁實際載入的檔，內容是 window.AUDIO_MANIFEST 物件
                  ＋ window.resolveAudioSrc(word, base) 輔助函式

網頁端邏輯（festival.html / bilingual.html / character.html 都一樣）：
  按鈕的 data-word → 查 AUDIO_MANIFEST 拿到檔名 → 播 mp3
  查不到 → 退回瀏覽器內建語音（speechSynthesis）當保底

────────────────────────────────────────
要重新產生 / 新增單字時
────────────────────────────────────────
產生腳本在（本機 scratchpad，非 repo）：
  tts_build/generate.py
裡面 FEST_WORDS / FEST_SENTENCES / CHARACTER / BIL_* 幾個清單，
內容要跟三個頁面裡 data-word 的字串「一模一樣」。改完跑：
  python3 generate.py
再把 out/ 底下的 *.mp3、manifest.json、manifest.js 複製到這個資料夾。

需要的工具：
  pip3 install --user edge-tts
  ffmpeg（本機已安裝於 /usr/local/bin）

換聲音：改 generate.py 的 VOICE。可用聲音列表：
  edge-tts --list-voices | grep en-
