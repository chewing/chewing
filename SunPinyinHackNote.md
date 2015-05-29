# n-gram #
  * lm\_sc.t3g.i386 is the trigram lexicon
  * dump
    * tslminfo -v -l dict.utf8 lm\_sc.t3g.i386
  * [Arpa format](http://www.speech.sri.com/projects/srilm/manpages/ngram-format.html)

  * 如果指定了ambiguous-id，则会将这6个字符作为一个AMBI-ID（由参数-a指定），输出到分词的结果中。然后跳过这6个字符，继续进行分词。当句子结束时，如果使用二进制格式输出，则会输出一个句子结束的ID（由参数-s指定）。最后得到的结果是:

> $ echo "为人民办实事的精神" | ./mmseg -d ../raw/dict.utf8 -f text -s 10  -a 9

> 

&lt;ambi&gt;

为人民办实事

&lt;/ambi&gt;

 的 精神

  * 那么，我们最终得到的分词结果中，所有的交集歧义都作为作为一个词AMBI-ID，相当于我们忽略了这部分信息（这个比例并不低）。这样在我们后面的统计中，绝大部分的3元组都可以保证是有意义和有价值的。进而训练得到的统计语言模型，能够排除交集歧义的影响。然后，可以这个模型，使用slmseg，重新对语料库进行分词，并计算新的语言模型。这一次，原来忽略的带有歧义的信息，我们也加以利用了。

# lexicon #
  * [SunPinyin代码导读（七）](http://blogs.sun.com/yongsun/entry/sunpinyin%E4%BB%A3%E7%A0%81%E5%AF%BC%E8%AF%BB_%E4%B8%83) 我们这里还要说明一下，在训练语言模型时对多音字词的处理。在处理语料库时，理想的情况下，应该将不同的读音视为不同的词ID。但是要准确地进行拼音标注，本身就十分困难，特别第一遍用FMM分词训练语言模型时。我们使用了下面的折衷方法：在词典文件dict.utf8中，我们对读音的常见程度进行了标记。例如“长”，它的两个读音“zhang”和“chang”都比较常见，分别被标为1；而“她”（ta），另一个读音“chi”则十分罕见，因此将其标为- 1。在训练时，我们将所有遇到的“她”，都认为是“ta”，然后为“chi”的读音分配一定的概率，并为其分配一个新的词ID。

# IME #
  * CIMIData
    * CPinYinTrie 詞典
    * CThreadlm n-gram

  * CIMIContext
    * setCoreData( CIMIData )
    * 斷詞演算法

  * CIMIView
    * attachIC( CIMIContext )
    * onKeyEvent()

# Data Structure #
  * CBone
    * m\_BoneType: 拼音 / 標點
    * m\_BoundaryType: 程式斷詞的邊界 / 使用者輸入的邊界
    * m\_pInnerData: 前一個bone的一些訊息

  * CSkeleton

# Lattice Search #
  * Bean search
    * bean = 32

# History Cache #