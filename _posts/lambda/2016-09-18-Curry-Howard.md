---
layout: post
title: "Lambda Calculus (6 - Curry-Howard correspondence)"
categories: lambda
---

這篇文章會討論有點不同的主題
從這個問題開始：
你要怎麼寫一個term
使得他的type為\\(\forall X. X\\)？

這是一個有點有趣的型別
屬於它的term必須要能被當作任何型別的值
顯然這有點無理
假如你用的是Haskell
或者是任何一個普通的程式語言
事實上可行的辦法是讓這個函數永遠不要回傳值
舉例來說讓它進入無窮迴圈
或者是直接終止程式
不過這些基本上都是*作弊*
不是嗎？
除了作弊之外
的確你是不應該有辦法寫出這樣的term的

有沒有可能設計一個*沒辦法作弊*的程式語言呢？
有的
沒辦法作弊這樣的特性事實上有個聽起來比較專業的名詞：**一致的**
前面我們介紹的所有lambda calculus都是一致的
也就是說不存在型別為\\(\forall X. X\\)的term
一般的程式語言是在lambda calculus的基礎上加了太多其它結構
讓你有辦法作弊
為什麼那些程式語言要被這麼設計呢？
因為作弊有時的確是好的
當你寫真正的程式時
你確實可能希望進入一個無窮迴圈
永遠不要結束函數
在先前介紹的各種最精簡的typed lambda裡面
所有函數都有NF
因此我們無法辦到這點

---

我要來直接切入一致性這樣的特性有什麼特別的意義了
接下來給出的資訊可能有點多
如果還沒辦法理解的話就一次背下來再繼續讀吧

二十世紀中的數學家們發現了一件事情
*型別系統*和*邏輯*是有直接的對應的
更精確地說是如此：
不同的type可以被視為不同的**命題**
而每個type的term則是它的**證明**
這樣的關係被稱為**柯里-霍華德對應**

先來解釋一下命題是什麼
一個命題可以被看為一個邏輯中可或不可證明的合法語句
假如一個命題無論在任何前提下都成立的話
則它被稱為**套套句**
既然套套句是命題
那麼便存在（至少）一個term的type是該命題對應到的type

舉個最早被發現的對應吧
由柯里在1934年發現
這樣的對應是：型別系統裡面的\\(\to\\)(函數型別)對應到了邏輯裡面的\\(\to\\)(蘊含)
如果讀者不熟悉邏輯裡面的蘊含的話
這邊稍微介紹一下
\\(A \to B\\)在邏輯裡面的意思是**\\(A\\)蘊含\\(B\\)**
換句話說就是由\\(A\\)的真實性可以推導至\\(B\\)的真實性
單單只用\\(\to\\)
我們就能建立某些套套句
舉例來說好了
像是\\(A \to A\\)(由任何事實能推導至它本身)
或者是\\(A \to (B \to A)\\)
(如果一個命題\\(A\\)是事實
那麼任何其它命題\\(B\\)是事實都能推導出\\(A\\)是事實)
咦
有沒有覺得有種熟悉的感覺？

事實上
這不就是\\(\mathbf{I}\\)和\\(\mathbf{K}\\)的type嗎？
這印證了套套句能被證明這樣的說法
但\\(\mathbf{I}\\)和\\(\mathbf{K}\\)的type前面的\\(\forall\\)又要怎麼解釋呢？
根據柯里-霍華德對應
\\(\forall\\)對應到了*對於所有type......*
type被對應到了命題
所以事實上也能解釋成*對於所有命題......*
這麼一來
\\(\mathbf{I}\\)的type能被解釋成*對於所有命題\\(A\\) \\(A\\)蘊含自身*
\\(\mathbf{K}\\)的type也能被類似的方式解讀
只要在前面加上*對於所有命題\\(A\\)和\\(B\\)*就可以了
不存在type為\\(\forall X. X\\)的term也因此會是型別系統裡很重要的特色
一旦系統*不一致*
任何命題都能被證明
而顯然對於一個邏輯來說這並不是我們想要的
在CoC裡面\\(\forall\\)和\\(\to\\)已經被統一
\\(\forall A. ...\\)指的事實上是\\((A: \star) \to ...\\)
其實我們也能有\\((A: Bool) \to ...\\)或\\((A: Nat) \to ...\\)
分別指*對於所有布林值*和*對於所有自然數*
依此類推

現在我們不知不覺進入了一階邏輯的領域
這是型別理論和傳統邏輯不一樣的地方
在傳統邏輯中
一階邏輯的變數和命題是兩種完全不同的東西
而在型別論中
命題只不過是\\(\star\\)的元素罷了
而述詞(接收值傳回命題的函數)或高階述詞也能被輕鬆定義

命題邏輯除了\\(\to\\)之外還有很多運算子
現在我將一一定義

首先
我把\\(\forall X. X\\)當作一個最無法被證明的命題
一旦它能被證明
任何命題都能被推導出來
\\(\forall X. X\\)在符號上因此被寫作\\(\bot\\)
顯然\\(\bot\\)蘊含任何命題
這邊來練習寫出第一個證明吧
我想要證明的是\\((A: \star) \to \bot \to A\\)
證明應該很顯而易見吧
只要寫出一個type為\\((A: \star) \to \bot \to A\\)的term就好了
而這樣的term是\\(\lambda A: \star. \lambda X: (A: \star) \to A. X A\\)
有趣的是我們調用了一個永遠不可能存在的函數(型別為\\((A: \star) \to A\\))
以符合我們想要證明的命題

\\(\bot\\)有時又被稱為**矛盾**
現在我們可以定義否定了
一個命題的否定能被證明代表它本身能推得矛盾
寫成符號的話

$$
\neg A \stackrel{def}{\equiv} A \to \bot
$$

如果你有一點邏輯的基礎的話
你可能會猜想
現在我們能用\\(\to\\)和\\(\neg\\)用你所想像的那套方式來定義其它邏輯運算子
很可惜這邊並不適用
接下來我要來解釋為什麼

在一般邏輯學的教科書上
你學到的那種邏輯被稱為**古典邏輯**
而我們在這邊考慮的是一套稍微不同的系統
被稱為**直構邏輯**
問題在於
在我們的詮釋下
邏輯系統和型別系統已經成為了一體兩面
而證明應該要能被當作程式調用
例如像是前面提到的\\(\mathbf{I}\\)和\\(\mathbf{K}\\)
除了作為命題的證明
還能被用於真正的程式中
可惜
古典邏輯裡面有些定理(套套句)完全無法被當作程式運行
例如像雙重否定律

$$
\neg \neg A \to A
$$

\\(\neg \neg A\\)依定義相等於\\((A \to \bot) \to \bot\\)
這是一個函數
要有適當的參數才能調用它
但事實是一個都沒有
所以直覺上是不可能從這個函數得到\\(A\\)的
換言之
不應該存在符合這個型別的程式

因此這邊要定義一個稍微比古典邏輯弱的系統
你可能會覺得這樣有點可惜
沒辦法證明一些原本能證明的定理
好消息是
只要假定雙重否定律
直構邏輯就會變成古典邏輯
這意味著你只要在需要的時候假定排中律就好了
只不過它們沒辦法被當作程式運行而已
而且直構邏輯還提供了比古典邏輯更強大的表達能力
就某種程度上
直構邏輯裡面的一切命題都是能被建構的

我接下來要說邏輯中的**或**和**且**怎麼在CoC中被定義
首先解釋*且*好了
\\(A\\)且\\(B\\)在邏輯上寫作\\(A \land B\\)
但一般型別系統中寫作\\(A \times B\\)
我們知道在CoC裡面幾乎只有函數這種東西而已
因此\\(A \times B\\)也應該被定義成某個函數
首先
我們知道如果\\(A\\)和\\(B\\)都能被證明
則\\(A \times B\\)也應該能被證明
用符號可以寫成這樣：

$$
A \to B \to A \times B
$$

上面的式子應被讀為\\(A \to B \to (A \times B)\\)
而非\\((A \to B \to A) \times B\\)
這邊要進入有點困難的部分了
來探討\\(A\\)、\\(B\\)、\\(A \times B\\)和一任意\\(C\\)的關係
要探討另一命題的原因是因為在CoC裡面唯一能使用一個值的方式就是把他丟進一個函數
定義\\(A \times B\\)時又勢必要用到\\(A\\)和\\(B\\)
而定義\\(A \times B\\)所用到的函數應當能回傳任何型別的值(下寫作\\(C\\))
所以\\(A \times B\\)可以被定義成：

$$
(C: \star) \to A \to B \to C ...
$$

這樣的定義還沒辦法滿足\\(A \to B \to A \times B\\)
因為一個隨意的\\(C\\)被導入了
假如把\\(A\\)和\\(B\\)丟進\\((C: \star) \to A \to B \to C\\)裡面
它會丟回一個type為\\(C\\)的term
怎麼辦呢？
因為\\(C\\)其實本質上是不重要的
不如我們就直接丟回\\(C\\)吧
把\\(A \times B\\)的定義改成\\((C: \star) \to (A \to B \to C) \to C\\)
而這就是\\(A \times B\\)的定義了

$$
A \times B \stackrel{def}{\equiv} (C: \star) \to (A \to B \to C) \to C
$$

接下來講\\(A \times B\\)在寫程式上有什麼意義
在程式的領域
\\(A \times B\\)被稱為一個**\\(A\\)和\\(B\\)的二元組**
它同時記錄了type為\\(A\\)的term和type為\\(B\\)的term兩者的資訊
\\(A \times B\\)本身是個type
要建構\\(A \times B\\)的term的方式如下

$$
(a, b): A \times B \\
(a, b) \stackrel{def}{\equiv} \lambda C: \star. \lambda f: A \to B \to C. f a b
$$

這樣的定義其實有點理所當然
它告訴我們可以把任何依賴\\(a\\)和\\(b\\)的函數丟進去以產生一個新的\\(C\\)的term
接著來介紹如何從\\((a, b)\\)中取回\\(a\\)和\\(b\\)兩者的資訊
稍微思考一下之後可以知道
只要把適當的\\(f\\)丟進去\\((a, b)\\)的定義就好了
要取得\\(a\\)的話用\\(\texttt{fst}\\)
要取得\\(b\\)的話用\\(\texttt{snd}\\)

$$
\texttt{fst}: A \times B \to A \\
\texttt{fst} \stackrel{def}{\equiv} \lambda t: A \times B. t A (\lambda a: A. \lambda b: B. a) \\

\texttt{snd}: A \times B \to B \\
\texttt{snd} \stackrel{def}{\equiv} \lambda t: A \times B. t B (\lambda a: A. \lambda b: B. b)
$$

其實有點像是循環論證啦
畢竟我們定義出二元組就是用來能讓\\(\texttt{fst}\\)和\\(\texttt{snd}\\)能被寫出來啊.....
一個雞生蛋蛋生雞的概念

接著來介紹邏輯中的*或*
\\(A\\)或\\(B\\)在邏輯上寫作\\(A \lor B\\)
但通常型別系統中寫作\\(A + B\\)
不囉唆直接給定義了：

$$
A + B \stackrel{def}{\equiv} (C: \star) \to (A \to C) \to (B \to C) \to C
$$

\\(A + B\\)的定義同樣會傳回一個任意的命題\\(C\\)
但不同的是它不需要同時接收\\(A\\)和\\(B\\)兩個參數
而是接收\\(A \to C\\)和\\(B \to C\\)
為什麼呢？
因為現在我們不要求\\(A\\)和\\(B\\)同時成立
而是其中一個成立就好了
假如是\\(A\\)成立好了
我們能把它丟給\\(A \to C\\)得到\\(C\\)
假如是\\(B\\)成立也類似
用這樣的寫法
我們只需要求兩者其中之一成立就好了

現在來講\\(A + B\\)在寫程式上頭的用途
它儲存了\\(A\\)或\\(B\\)其中一者的term
在\\(A \times B\\)中
要建構一個term只需要一個函數
要獲得它的內容則有\\(\texttt{fst}\\)和\\(\texttt{snd}\\)兩種方式
\\(A + B\\)則相反
有兩種方式能建構一個type為\\(A + B\\)的term
但要使用它只有一種方式

要獲得\\(A + B\\)的term的第一個方式是\\(\texttt{inl}\\)
以\\(A + B\\)來說
\\(\texttt{inl}\\)代表的是它的內容事實上是左邊的\\(A\\)
第二個方式則是\\(\texttt{inr}\\)
代表的是它的內容事實上是右邊的\\(B\\)

$$
\texttt{inl}: A \to A + B \\
\texttt{inl} \stackrel{def}{\equiv} \lambda a: A. \lambda C: \star. \lambda f: A \to C. \lambda g: B \to C. f a \\

\texttt{inr}: B \to A + B \\
\texttt{inr} \stackrel{def}{\equiv} \lambda a: A. \lambda C: \star. \lambda f: A \to C. \lambda g: B \to C. g a
$$

至於要如何使用\\(A + B\\)
\\((C: \star) \to (A \to C) \to (B \to C) \to C\\)這個type說得很清楚了
我們要決定一個目標type
就叫他\\(T\\)好了
然後提供一個\\(A \to T\\)的函數和一個\\(B \to T\\)的函數
把它丟給\\(A + B\\)的term後就會拿回一個\\(T\\)

至於表示兩個命題相等的雙箭頭\\(\leftrightarrow\\)
則可以被定義成\\(A \leftrightarrow B \stackrel{def}{\equiv} (A \to B) \times (B \to A)\\)
命題邏輯的部分就到此告一段落了

在一階邏輯中
還有另外一個符號用來表示*存在某個值使得一述詞成立*
相對於*對於所有值一述詞成立*
邏輯符號上寫作\\(\exists x. P\\)
在型別論裡面
*對於所有值一述詞成立*的對應是\\(\Pi\\)-型別
也就是回傳type裡面可使用輸入值的函數
是原本\\(\to\\)的推廣
*存在某個值使得一述詞成立*的對應則是\\(A \times B\\)的推廣
其中\\(B\\)可以*依賴*type為\\(A\\)的term
這樣的型別被稱為\\(\Sigma\\)-型別
符號上則寫作

$$
\sum\limits_{a: A} B
$$

其中\\(a\\)被稱為\\(\Sigma\\)的綁定變數
和\\(\Pi\\)-型別一樣
\\(\Sigma\\)-型別中綁定變數的型別也不一定要是\\(\star\\)
而可以是一個一般的type
舉例來說
如果你想表示*對於某個自然數一述詞成立*
你可以寫\\(\sum\limits_{n: Nat} B\\)

要怎麼在CoC裡定義它呢？
因為\\(\Sigma\\)-型別是\\(\times\\)的推廣
\\(\Sigma\\)-型別的定義方法和\\(\times\\)的也類似
只是二元組裡面的第二個物體的type必須要能提到第一個物體的值
事實上我們只要把原本定義裡面的\\(A\\)改成可以被依賴的形式就好了：

$$
\sum\limits_{a: A} B \stackrel{def}{\equiv} (C: \star) \to ((a: A) \to B \to C) \to C
$$

一旦\\(a\\)能被依賴
\\(B\\)這個type中便可以使用到\\(a\\)
如果要建構一個\\(\Sigma\\)-型別的term
我在此使用和普通\\(\times\\)型別一樣的語法：

$$
(a, b): \sum\limits_{a: A} B \\
(a, b) \stackrel{def}{\equiv} \lambda C: \star. \lambda f: (a: A) \to B \to C. f a b
$$

\\(\texttt{fst}\\)和\\(\texttt{snd}\\)的定義則如下：

$$
\texttt{fst}: (\sum\limits_{a: A} B) \to A \\
\texttt{fst} \stackrel{def}{\equiv} \lambda t: \sum\limits_{a: A} B. t A (\lambda a: A. \lambda b: B. a) \\

\texttt{snd}: (t: \sum\limits_{a: A} B) \to B[a := \texttt{fst} \: t] \\
\texttt{snd} \stackrel{def}{\equiv} \lambda t: \sum\limits_{a: A} B. t (B[a := \texttt{fst} \: t]) (\lambda a: A. \lambda b: B. b)
$$

以程式的角度來探討
\\(\Sigma\\)-型別可以被想成是抹去type中一部份的資料
舉例來說好了
假設我們的系統裡有個叫\\(Array\\)的type
\\(Array\\)的型別是\\(\star \to Nat \to \star\\)
意思是它接收一個型別和一個自然數
建構一個元素為那個型別且長度等同於那個自然數的陣列
假如我想要寫一個函數
把原本陣列裡重複的值刪除
你不能把它的型別寫作\\((T: \star) \to (n: Nat) \to Array \\: T \\: n \to Array \\: T \\: n\\)
這樣寫的話
你傳入和傳回陣列的\\(n\\)必須是同一個值
問題是一旦你刪除了陣列裡的某些元素
陣列的長度就會縮短！
事實上應該被表達的是回傳的\\(Array\\)的長度是某個特定的值
但我們不確定那個值是什麼
換句話說
我想抹去type中長度的資料
所以我應該用\\(\Sigma\\)-型別這麼寫：

\\((T: \star) \to (n: Nat) \to Array \\: T \\: n \to \sum\limits_{m: Nat} Array \\: T \\: m\\)
