---
layout: post
title: "Lambda Calculus (1 - untyped lambda)"
categories: lambda
---

來寫教學吧
畢竟我最喜歡寫教學了...XD
這次要來說的是untyped lambda

這系列文章主要會有兩個特點

1. 不需閱讀程式碼
   會盡量用文字清楚描述概念
   而不是只提供程式碼
   原因有兩個
   第一是我用的程式語言不一定每個人都懂
   第二是我覺得文字比程式碼好讀

2. 先提供範例 再描述實作
   先從直觀的範例開始
   再解釋要怎麼做出來
   不然看了容易霧煞煞

# 定義

什麼是untyped lambda呢？
在提untyped lambda是什麼之前
我們要先知道什麼是lambda calculus
lambda calculus和微積分(也叫calculus)是完全不同的東西

lambda caculus是一類很小的程式語言
可以這麼說
它把一般程式語言最精華的部分取出來
而得到一個很廣泛而抽象的概念
在這個簡單的概念上
我們可以建構許多更高層次的東西
而untyped lambda就是沒有型別的lambda calculus
既然沒有型別
也就不用進行型別檢查
直接餵給解譯器跑就好了

這樣說好像很抽象
就算知道了lambda calculus是很小的語言
你一定想問
lambda calculus裡面有什麼樣的構造呢？
在這篇文章裡面
我們要提的untyped lambda只有三種構造而已
分別是：

1. 變數
   通常寫成\\(x\\), \\(y\\), \\(z\\)
   一般來說三個字母應該就夠用了
   不過事實上untyped lambda裡面應該提供無限多個變數
   就像你在一般的程式語言裡面能宣告任意多個變數一樣

2. lambda
   這是最重要的地方
   lambda把函數的概念做了抽象
   任何lambda都是只接收一個變數
   吐出一個運算式的函數
   舉例來說
   像是\\(x \mapsto x\\)
   這是最簡單的lambda
   它是一個接受任何參數
   然後直接把參數原封不動吐出來的函數

3. 函數調用
   我們已經能夠定義函數了
   接下來還要能使用函數
   通常我們把兩個運算式寫在一起
   就代表了我們把後者當作參數傳給前者的函數中

......還是很抽象對吧？
現在我要再用更具體的例子解釋
你知道函數是什麼吧？
我們通常宣告函數的方式是寫成這樣

$$
f(x) = x
$$

以上的函數接受一個名為`x`的變數
然後將它原封不動地吐出來

lambda在做的事情是：
它提供了函數的另外一種寫法
\\(f(x) = x\\)這種寫法的問題在於
我們宣告一個函數時一定要給它一個名字
為了用更小的語言表達函數的概念
我想乾脆把函數的名稱省去了
現在我要提供函數的另一種寫法：

$$
x \mapsto x
$$

而以上這種「沒有名字的函數」就被叫做lambda

要把\\(5\\)丟進\\(f\\)裡面
一般來說
你會寫成\\(f(5)\\)
而一旦換成了lambda
原本的函數調用便可以寫成這樣

$$
(x \mapsto x)(5)
$$

這樣應該有更清楚吧？

順帶一提
在lambda calculus裡面
我們通常省略函數呼叫時參數周圍的括號
因此上述的函數調用又能被寫成\\((\lambda x. x) 5\\)
你一定會想問
這個\\(\lambda x. x\\)又是什麼東西
其實這只不過是lambda calculus裡面較常用的匿名函數寫法而已
和\\(x \mapsto x\\)意思是一樣的
以後我們都會用\\(\lambda\\)這種寫法

我現在要用更嚴格的方式說明一次
何謂untyped lambda的運算式
和常見的數學定義一樣
底下將會使用到遞迴定義

lambda運算式包含了三種東西：

1. 變數 說過啦

2. 對所有變數名稱\\(x\\)
   和所有運算式\\(t\\)
   \\(\lambda x. t\\)是一個運算式

3. 對所有運算式\\(t_1\\)
   和所有運算式\\(t_2\\)
   \\(t_1 t_2\\)是一個運算式

4. 除上述之外
   沒有任何其它東西是運算式

用Haskell可以寫成這樣：

```haskell
newtype Symbol = Symbol String
data Expr = Var Symbol
          | Lam Symbol Expr
          | App Expr Expr
```

# 慣例

按照慣例
函數調用是左結合的
舉例來說
\\((\lambda x. \lambda y. x) z w\\)代表的是\\(((\lambda x. \lambda y. x) z) w\\)
(糟糕 我發現三個變數不夠用了)
順便來解釋一下這個\\(\lambda x. \lambda y. x\\)是什麼
我們通常把這個運算式叫做\\(\mathbf{K}\\)
因此上面的運算式又能寫成\\(\mathbf{K} z w\\)
\\(\mathbf{K}\\)接收了一個變數
傳回另一個接收一個變數的函數
而後者傳回前者接收的變數
換句話說
較內部的函數接收到的參數是被省略的
事實上
我們能用更容易理解的方式解釋\\(\mathbf{K}\\)
當兩層lambda套在一起時
我們可以把它「當作」是一個接受兩個參數的函數
因此
\\(\mathbf{K}\\)可以被想成是
「接受兩個參數
而返回第一個參數的函數」
這樣模擬多變數函數的方法叫作柯里化(currying)
有些人也會把\\(\mathbf{K}\\)寫成\\((\lambda x y. x)\\)
注意\\(\lambda\\)後面寫了兩個變數
但事實上它只不過是種語法糖罷了
並不是種新的結構
事實上和原本的\\(\mathbf{K}\\)還是一樣的

除了\\(\mathbf{K}\\)之外
其它有名字的函數還有\\(\mathbf{I}\\)
也就是上面提供的\\((\lambda x. x)\\)
因為常常用到所以就有了個名字

# 資料型態

前面有提到了\\(\mathbf{I}\\: 5\\)
你可能會好奇
這個\\(5\\)又是什麼呢？
畢竟\\(5\\)並不是untyped lambda裡面的結構
事實上它只是某個lambda運算式的簡寫而已
並不是系統內的變數
我們前面提到的\\(\mathbf{K}\\)和\\(\mathbf{I}\\)也都只是簡寫
你可以想成是這些變數會在C預處理器中被定義
預處理過後就會被替換成真正的運算式

那\\(5\\)所代表的運算式又是什麼？
先別急
我會先提布林代數的實作方法
之後再提自然數

## 布林代數

$$
\begin{array}{lcl}
\mathbf{TRUE}  & = & \mathbf{K} \\
\mathbf{FALSE} & = & \lambda x y. y
\end{array}
$$

\\(\mathbf{TRUE}\\)傳回兩個參數中的第一個
\\(\mathbf{FALSE}\\)傳回第二個
因此要寫一個\\(\mathbf{IF}\\)是不難的

$$
\mathbf{IF} = \lambda p x y. p x y
$$

\\(\mathbf{IF}\\)只要把後面兩個參數丟給第一個參數就好了
所以\\(\mathbf{IF \\: TRUE} \\: x y = x\\)
而且\\(\mathbf{IF \\: FALSE} \\: x y = y\\)

(未撰寫)

# \\(\beta\\)-歸約

\\(\beta\\)-歸約是解譯lambda很重要的一步
它的用途是真正把函數調用到其它參數上的這個過程完整解釋清楚
\\(\beta\\)-歸約主要告訴我們的是
假設你有一個運算式\\(t_1 t_2\\)
而\\(t_1\\)是個lambda \\(\lambda x. t_3\\)
則調用後的結果是把\\(t_3\\)中出現的\\(x\\)取代成\\(t_2\\)
舉例來說
像\\(\mathbf{I} \\: 5 = 5\\)
還有\\(\mathbf{K} \\: 2 \\: 3 = 2\\)
我們把將\\(t_3\\)中的變數名稱\\(x\\)改寫成\\(t_2\\)這個替換的動作寫成\\(t_3[x := t_2]\\)
值得一提的是
\\(t_3[x := t_2]\\)不只是單純把\\(t_3\\)中出現的所有\\(x\\)都改寫成\\(t_2\\)
事實上的狀況可能會比你想像中複雜一些

為什麼？
試想\\((\lambda x. \lambda x. y) y z\\)這個例子
如果只看最左邊的\\(\lambda x. \lambda x. y\\)
你應該會預期無論這個函數接收了哪兩個參數
最後都應該傳回\\(y\\)
但假設我們用最天真的方式將\\(x\\)改寫成\\(y\\)
你會發現\\((\lambda x. \lambda x. y) y\\)變成了\\((\lambda x. y)[x := y]\\)也就是\\(\lambda y. y\\)
而\\((\lambda y. y) z = z\\)
當然啦
\\(\lambda x. y\\)中的\\(x\\)只是個變數名稱而已
不是一個完整的運算式
如果把\\(y w\\)代入\\(x\\)很明顯是不合理的
因此我們對於\\(t_3[x := t_2]\\)的定義肯定要更加精確

我們現在試著做些調整：
不變換*綁定變數*的名稱
什麼是綁定變數？
綁定變數就是\\(\lambda\\)名後面緊接著的變數名稱
若不變換綁定變數
我們可以如下定義\\(t_3[x := t_2]\\)：

$$
\begin{array}{lcl}
x[x:=t_1] & = & t_1 \\
y[x:=t_1] & = & y & \mbox{if } x≠y \\
(λy. t_2)[x:=t_1] & = & λy. (t_2[x:=t_1]) \\
(t_2 t_3)[x:=t_1] & = & t_2[x:=t_1] t_3[x:=t_1]
\end{array}
$$

上面的式子應該不難讀吧
第一行和第二行代表的是
當遇到變數時
如果變數等於要取代掉的變數
則把變數取代掉
如果不是要取代掉的變數
原封不動的送回它
第三行代表的是
如果遇到了lambda
只取代lambda內部運算式的變數而非綁定變數
第四行說如果遇到了函數調用
則分別取代左右兩邊運算式中的變數

這樣就結束了嗎？
並沒有
我們的式子還是有點問題
因為綁定變數不會被取代
所以\\((\lambda x. \lambda x. x) y z\\)會等於\\(y\\)
而照理，來說它應該會等於\\(z\\)的
為什麼？
因為最右邊的\\(x\\)事實上應該要代表中間的那個\\(x\\)
而非最左邊的\\(x\\)
最左邊的\\(x\\)就像是被中間的\\(x\\)「遮蔽」了一樣
但我們的取代公式卻無法考量到這一點

我們似乎還是取代了太多變數
這次問題出在了\\((\lambda x. x)[x := t_1]\\)上
事實上
當把\\(x\\)取代成\\(t_1\\)時遇到了另一個以\\(x\\)為綁定變數的lambda時
我們大可不必取代掉裡面的任何\\(x\\)
因為那裡面的\\(x\\)早就不是我們熟知的那個\\(x\\)了

因此我們的公式要變得更複雜：

$$
\begin{array}{lcl}
x[x:=t_1] & = & t_1 \\
y[x:=t_1] & = & y & \mbox{if } x \neq y \\
(λy. t_2)[x:=t_1] & = & \begin{cases}
                         \lambda y. t_2 & \mbox{if } x=y \\
                         \lambda y. (t_2[x := t_1]) & \mbox{if } x \neq y
                         \end{cases} \\
(t_2 t_3)[x:=t_1] & = & t_2[x:=t_1] t_3[x:=t_1]
\end{array}
$$

這樣的式子...呃...還是有問題
問題又出在lambda上
這次考慮這個運算式
$$
(\lambda x. \lambda y. x) y z
$$
它應該等於\\(\mathbf{K} y z\\)
也就是\\(y\\)
但我們把\\(y\\)丟進\\(\lambda x. \lambda y. x\\)裡面
答案卻變成了\\(\lambda y. y\\)
而\\(\mathbf{I} z = z\\)！
這麼看起來
似乎怎麼做都是不對的
難道真的沒有解決方法嗎？

答案是有的
雖然那樣的方法有點「不數學」
在介紹那樣的方法前
我們要先解釋何謂*自由變數*
先告訴大家吧
導致\\((\lambda y. x)[x := y]\\)的取代發生錯誤的原因就是我們沒有分清楚什麼是自由變數

## 自由變數

來整理一下每次遇到的問題
第一次我們犯的錯誤是
取代不該被取代的綁定變數名稱
第二次我們犯的錯誤是
沒有注意到lambda內部同名的綁定變數會「遮蔽」到外部的綁定變數
第三次犯的錯誤是
原本右邊運算式的自由變數會指到左邊lambda的綁定變數上

現在要解釋自由變數到底是什麼
自由變數是「可能會不小心指向別的綁定變數的變數」
來看看上面提到的\\((\lambda x. \lambda y. x) y\\)
這之所以會有問題
是因為原本最右側的自由變數\\(y\\)指向了內部的綁定變數\\(y\\)
同樣的\\((\lambda x. \lambda y. x) (y z)\\)也會有問題
因為取代後\\(y z\\)中的\\(y\\)也會指向綁定變數\\(y\\)
\\((\lambda x. \lambda y. x) (\lambda y. y)\\)反而沒問題了
\\((\lambda y. x)[x := (\lambda y. y)] = \lambda y. \lambda y. y\\)
這是正確的取代
因為最右側的\\(y\\)原本指向中間的\\(y\\)
取代之後還是指向中間的\\(y\\)
因此\\(\lambda y. y\\)中的\\(y\\)是「免疫於指向其它綁定變數」的
也就是說
\\(\lambda y. y\\)中的\\(y\\)並非自由變數

有了大概的概念之後
我要來講比較嚴謹的定義
我們把\\(FV\\)定義成一個接受一個lambda運算式
傳回它所有自由變數的集合的函數
\\(FV\\)的完整定義如下：

$$
\begin{array}{lcl}
FV(x) & = & \{ x \} \\
FV(\lambda x. t) & = & FV(t) \backslash \{ x \} \\
FV(t_1 t_2) & = & FV(t_1) \cup FV(t_2)
\end{array}
$$

其中\\(\backslash\\)代表差集

回到取代上
現在的問題只剩下\\((\lambda y. t_2)[x := t_1]\\)而且\\(x \neq y\\)以及\\(y \in FV(t_1)\\)的情況
最不數學的部分要來了
解決這個問題的方法很簡單
就是隨便找一個沒用過的變數
就叫它\\(w\\)好了
先把原本左邊的lambda改成\\(\lambda w. (t_2[y := w])\\)
然後再做原本要做的取代
\\(t_2[y := w]\\)是一定不會遇到問題的
因為\\(w\\)是一個全新的變數
所以\\(w \notin FV(t_2)\\)絕對會成立
之後再取代也絕對不會出現問題
因為\\(w \notin FV(t_1)\\)
事實上我們挑選的\\(w\\)也不一定要是全新的
只要滿足\\(w \notin FV(t_1) \cup FV(t_2)\\)就好了

取代的部分就在此告一段落

# 歸約策略

我們知道了要怎麼用對運算式進行\\(\beta\\)-歸約
接下來我要探討的是
要在運算式中的「哪裡」進行\\(\beta\\)-歸約
在這方面
我們在實作上有好幾個選擇

先解釋什麼是NF(Normal Form)
假設一個運算式所有能作\\(\beta\\)-歸約的地方都做了歸約
那麼它的結果便被叫做NF
換句話說
在NF裡所有的lambda後面都不應該有其它運算式

除了NF之外
我們還能選擇不要歸約所有運算式
一般來說有兩個可以不要歸約的狀況

1. lambda內
   舉例來說
   因為\\(\mathbf{I} x = x\\)
   \\(\lambda x. \mathbf{I} x\\)的NF是\\(\lambda x. x\\)
   但當我們不歸約lambda內的運算式時
   \\(\lambda x. \mathbf{I} x\\)便不用再被歸約

2. 參數上
   在**嚴格歸約**中
   lambda的參數總是比函數調用早做歸約
   相反的
   在**非嚴格歸約**中
   我們不會提早歸約lambda的參數
   舉個例子吧
   這邊我們要介紹一個新的運算式\\(\Omega\\)
   \\(\Omega = (\lambda x. x x)(\lambda x. x x)\\)
   這個運算式沒有NF
   因為\\((x x)[x := (\lambda x. x x)] = (\lambda x. x x)(\lambda x. x x)\\)
   它歸約的結果是它自己！
   \\(\Omega\\)不管被歸約幾次都還能繼續被歸約
   因此\\(\Omega\\)沒有NF
   現在考慮\\(\mathbf{K \: I} \: \Omega\\)
   這個運算式在非嚴格歸約中的結果為\\(\mathbf{I}\\)
   但在嚴格歸約中則沒有結果
   因為嚴格歸約會先歸約參數
   當它算出\\(\mathbf{K \: I}\\)的結果之後
   他會努力開始歸約\\(\Omega\\)
   而這樣的歸約永遠也做不完
   你可能會好奇
   有沒有歸約策略可以盡可能把所有能歸約的運算式做完
   而不要遇到無窮迴圈
   答案是
   沒有
   因為untyped lambda是[圖靈完全](https://zh.wikipedia.org/wiki/%E5%9C%96%E9%9D%88%E5%AE%8C%E5%82%99%E6%80%A7)的
   而這相當於判斷[停機問題](https://zh.wikipedia.org/wiki/%E5%81%9C%E6%9C%BA%E9%97%AE%E9%A2%98)

實作上的話
建議參考[Simpler, Easier!](http://augustss.blogspot.tw/2007/10/simpler-easier-in-recent-paper-simply.html)的最前段
原本想一行一行解釋自己的實作
但想說網路上已經有了
就算囉XD
但要懂Haskell就是了