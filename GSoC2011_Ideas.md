# Motivation #

Chinese input methods like Chewing are typically used everyday, and there is always room for improvements no matter the underlying environment is.  The reason why Chewing project would like to participate in GSoC is to invite more potential developers to improve the quality and usability for essential system software components (input method engines) and make them feel a real sense of fulfillment while improving Chewing input method is used in large amount of devices/computers everyday.

# Ideas #

1. To decouple libchewing-data from libchewing engine completely, libchewing needs to read and look up the data from dictionary files dynamically.  At present, libchewing supports the binary data format, but it can only load one directory without re-enabling other dictionaries at run-time.  This task is to support multiple dictionaries dynamically.

2. 多個字典同時使用，目前使用單一字典的缺點就是龐大的字典可能不適合所有  的場合，可以使用多個字典會帶來許多彈性，甚至線上字典也可以直接整合進來。現在的 code base 中，其實已經有兩種字典，也就是系統字典與使用者字典，可以在這個的基礎上發揮。
bonus: 簡化 API，把搜尋字典的方式變成搜尋路徑，如此一來只要是在 $CHEWING\_DICT\_PATH 內的字典都可以使用。

caveat: 需考慮多字典之間的干擾以及統計學上的意義

3. 分離字典的索引以及內容，目前字典的方式是把索引與詞庫建立為樹狀結構，但是索引只能用注音，不能反查等等，某些應用上不太方便。若是建立一組公開的 API 供查詢字典，那麼要實做無聲調拼音或是其他輸入法的智慧組字等等，或是聯想詞輸入，都可以直接利用酷音的字典。

4. 可以分開使用的 keyboard layout。這可以算是把 libchewing 區分為 輸入、虛擬輸入法、斷詞選字、字典查詢 四個部件的其中一部分。目前有些輸入法需要特殊的輸入方式，如許氏和倚天26等，若是可以方便的自訂輸入方式，實驗各種鍵盤對應等等，應該很不錯。