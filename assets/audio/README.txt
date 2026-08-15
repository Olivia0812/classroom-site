把發音音檔放在這個資料夾，檔名要跟下面對應：

雙語魔法屋（pages/bilingual.html）
harvest.mp3
lantern.mp3
gratitude.mp3

節慶萬花筒（pages/festival.html）
mooncake.mp3
lantern.mp3（跟雙語魔法屋共用同一個字，放一次就好）
reunion.mp3

品格超能力（pages/character.html）
honesty.mp3
responsibility.mp3
perseverance.mp3
courage.mp3
respect.mp3
gratitude.mp3（跟雙語魔法屋共用同一個字，放一次就好）
politeness.mp3
helping-others.mp3
sharing.mp3
empathy.mp3
teamwork.mp3

之後每次換單字，把新的 mp3 放進來，檔名對應網頁裡
每個 <button class="audio-btn" data-audio="..."> 的路徑就可以了，
不用改任何程式碼。

在真的 mp3 檔放進來之前，按鈕會自動改用瀏覽器內建的
語音朗讀（Web Speech API）唸出單字，所以現在點下去就已經
聽得到發音了，不用等音檔完成。
