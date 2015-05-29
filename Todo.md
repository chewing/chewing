# Todo for porting SunPinYin #

### step 1: 聲調 ###
  1. modify "sunpinyin/slm/raw/dict.utf8" (加入聲調)
  1. 重新產生 "sunpinyin/ime/data/pydict\_sc.bin.i386" 並測試是否能正確運作
  1. modify imi\_view\_modern，使可以輸入聲調

### step 2: 繁體化 ###
> #### 方法1 ####
    * 使用dict.utf8
    * 逆向工程 lm\_sc.t3g.i386 將其轉回原始格式，再進行繁體化

> #### 方法2 ####
    * 使用dict.utf8
    * 自行用語料重新訓練n-gram (lm\_sc.t3g.i386)
    * 目前可得的只有簡體的搜狗語料 http://www.sogou.com/labs/dl/t.html

> #### 方法3 ####
    * 不使用dict.utf8，自行用libtabe，並自行收集未斷詞的語料