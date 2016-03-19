---
layout: post
title: "Lambda Calculus (4 - system Fω)"
categories: lambda
---

開門見山
system F導入了type到term的函數
system Fω則再導入了type到type的函數
現在我們要導入*type的型別*
還記不記得一開始在用untyped lambda的時候是沒有型別的
這麼一來能寫出\\(\Omega\\)之類的無窮迴圈
假如type到type的函數是無型別的話
那不就也能在type階層上跑無窮迴圈了嗎QAQ
不......

為你隆重介紹 **kind**

<!--more-->

kind是type的型別
首先
我們有一個最基礎的kind
叫作\\(\star\\)(就是一個星號沒錯)
英文讀成star
所有我在system F裡面提過的type都屬於這個kind
還記得前面的判決吧
那時的\\(\star\\)就是這樣來的
除此之外
還能用箭頭\\(\to\\)建構更複雜的kind
有沒有覺得這句話很眼熟？
對
事實上可以發現
我們建構的kind系統非常接近STLC的type系統
只是更往上了一層而已
原先type階層的\\(Base\\)對應到了kind階層的\\(\star\\)
而type階層的\\(\to\\)對應到了kind階層的\\(\to\\)
啊對了提一下
目前type階層的\\(\to\\)和kind階層的\\(\to\\)還是不同的東西喔
它們只是長得一樣而已
其實運作在不同階層的是不同的箭頭

要怎麼寫一個type到type的函數呢
舉個最簡單的例子
\\(\emptyset \vdash (\lambda A: \star. A): \star \to \star\\)
這相當於STLC中的\\(\emptyset \vdash (\lambda x: Base. x): Base \to Base\\)
這邊我也重用了\\(\lambda\\)符號
讓它能代表一個type到type的函數
事實上我們能在system Fω裡能多定義的函數也就是STLC的那些
只是*高了一層*而已

# 定義

$$
\begin{array}{rcl}
term(t) ::= & \mathbf{var} (x) \\
          | & \lambda x: T. t \\
          | & t t \\
          | & \Lambda X: K. t \\
          | & t T \\
type(T) ::= & \mathbf{Var} (X) \\
          | & \lambda X: K. T \\
          | & T T \\
          | & T \to T \\
          | & \forall X: K. T \\
kind(K) ::= & \star \\
          | & K \to K \\
\end{array}
$$

和system F 差了哪些呢？

1. \\(\Lambda\\)和\\(\forall\\)的綁定變數上多了一個kind的標記
   所以現在可以把一個型別是\\(\star \to \star\\)的type丟到\\(\Lambda\\)裡

2. 增加了type到type的lambda和函數調用

3. kind階層 上面提過囉

就是這樣囉！

# 歸約

system Fω一樣是強規範化的

# type checking

先整理一下之前是怎麼進行type checking的
首先是untyped lambda
我們不用進行任何type checking

| 變數                | lambda           | 函數調用 |
|:----------------------|:-------------------|:-----------|
| term(t):              |                    |            |
| \\(\mathbf{var}(x)\\) | \\(\lambda x. t\\) | \\(t t\\)  |

接著是STLC
我們需要3條推導規則

| 變數                   | lambda              | 函數調用           | 函數型別               | 其它                 
|:-----------------------|:----------------------|:---------------------|:-----------------------|:---------------------
| term(t):               |                       |                      |                        |
| \\(\mathbf{var}(x)\\)  | \\(\lambda x :T. t\\) | \\(t t\\)            |                        |
| \\(\uparrow(var)\\)    | \\(\uparrow(abst)\\)  | \\(\uparrow(appl)\\) |                        |
| type(T):               |                       |                      |                        |
|                        |                       |                      | \\(T \to T\\)          | \\(Base\\)
|                        |                       |                      | \\(\uparrow\\)(不用規則) | \\(\uparrow\\)(不用規則)

然後是6條規則的system F

| 變數                   | lambda               | 函數調用             | 函數型別           |
|:-----------------------|:-----------------------|:-----------------------|:---------------------|
| term(t):               |                        |                        |                      |
| \\(\mathbf{var}(x)\\)  | \\(\lambda x.:T t\\)   | \\(t t\\)              |                      |
| \\(\uparrow(var)\\)    | \\(\uparrow(abst)\\)   | \\(\uparrow(appl)\\)   |                      |
|                        | \\(\Lambda X. t\\)     | \\(t T\\)              |                      |
|                        | \\(\uparrow(abst_2)\\) | \\(\uparrow(appl_2)\\) |                      |
| type(T):               |                        |                        |                      |
| \\(\mathbf{Var}(X)\\)  |                        |                        | \\(T \to T\\)        |
| \\(\uparrow\\)(不用規則) |                        |                        | \\(\uparrow(form)\\) |
|                        |                        |                        | \\(\forall X. T\\)   |
|                        |                        |                        | \\(\uparrow(form)\\) |

接著可以講system Fω了

| 變數                                  | lambda               | 函數調用             | 函數型別              | 其它
|:----------------------------------------|:-----------------------|:-----------------------|:-----------------------|:---
| term(t):                                |                        |                        |                        |
| \\(\mathbf{var}(x)\\)                   | \\(\lambda x:T. t\\)   | \\(t t\\)              |                        |
| \\(\uparrow(var), (weak_1), (weak_2)\\) | \\(\uparrow(abst)\\)   | \\(\uparrow(appl)\\)   |                        |
|                                         | \\(\Lambda X: K. t\\)  | \\(t T\\)              |                        |
|                                         | \\(\uparrow(abst_2)\\) | \\(\uparrow(appl_2)\\) |                        |
| type(T):                                |                        |                        |                        |
| \\(\mathbf{Var}(X)\\)                   | \\(\lambda X: K. T\\)  | \\( T T\\)             | \\(T \to T\\)            |
| \\(\uparrow(var_T)\\)                   | \\(\uparrow(abst_T)\\) | \\(\uparrow(appl_T)\\) | \\(\uparrow(arrow_T)\\)  |
|                                         |                        |                        | \\(\forall X: K. T\\)    |
|                                         |                        |                        | \\(\uparrow(forall_T)\\) |
| kind(K):                                |                        |                        |                        |
|                                         |                        |                        | \\(K \to K\\)            | \\(\star\\)
|                                         |                        |                        | \\(\uparrow\\)(不用規則) | \\(\uparrow\\)(不用規則)

注意上面一共有12條規則
除此之外還有一條\\((conv)\\)用作特殊用途
現在語境裡面可以有兩種東西
一個term的型別是一個type的判決
和一個type的型別是一個kind的判決
接下來我一個一個規則討論

所有kind都是合法的
因此kind階層沒有規則
type階層則有5個規則
分別對應到建構type的5種方式
它們分別是......

$$
\begin{array}{lcl}
(var_T) & \Gamma \vdash X: K & \mbox{if } X: K \in \Gamma \\
(appl_T) & \dfrac{\Gamma \vdash T_1: K_1 \to K_2 \qquad \Gamma \vdash T_2: K_1}{\Gamma \vdash T_1 T_2: K_2} \\
(abst_T) & \dfrac{\Gamma, X: K_1 \vdash T_2: K_2 }{\Gamma \vdash (\lambda X: K_1. T_2): K_1 \to K_2}
\end{array}
$$

注意這3條規則和STLC的3條規則的相似性
其它我不解釋

$$
\begin{array}{lcl}
(arrow_T) & \dfrac{\Gamma \vdash T_1: \star \qquad \Gamma \vdash T_2: \star}{\Gamma \vdash T_1 \to T_2: \star} \\
(forall_T) & \dfrac{\Gamma, X: K_1 \vdash T_2: \star}{\Gamma \vdash \forall X: K_1. T_2} \\
\end{array}
$$

這2條規則取代了先前的\\((form)\\)
為什麼要分成2條呢？
因為現在我們有了更多合法的type
所以我們必須更精確地描述什麼樣的type才是正確的
先看看\\((arrow_T)\\)
這條規則很好理解
要是\\(T_1\\)和\\(T_2\\)都是合法的*一般* type
則\\(T_1 \to T_2\\)也是合法的一般type
什麼是一般的type呢？
要是存在一個term
它的型別是某type
則上述的某type是個一般type
為什麼一定要是一般type呢？
假如lambda中綁定變數的的型態不是一個一般type
則我們就沒辦法調用那個lambda
因為我們無法以任何值作為參數
有什麼非一般type的例子？
例如像\\(\lambda A: \star. A\\)就不是一般type
它的kind不是\\(\star\\) 而是\\(\star \to \star\\)

然後是\\((forall_T)\\)
我們反過來讀
當遇到\\(\forall\\)時
我們把綁定變數丟到語境裡面檢查內層必須是個一般type
現在我把type階層上的規則都說完了

然後是term層級的規則
注意到了現在term變數的規則有兩條
也就是說沒辦法再*由下往上看*了
因為由下往上看這個方法是建立在只有一個規則能導向結論的判決時
要是有兩個以上的可能性
你就無法知道哪個規則會被實際運用
因此這邊我會由上往下看

先講\\((var)\\)
這個規則的理念是這樣的
如果一個term的變數\\(x\\)的type是\\(T\\)
則這個\\(T\\)必須出現在語境的稍早
且\\(T\\)要是個一般type
雖然我在前面並沒有強調
但語境其實是個*有序表*
它是有順序的
每次使用\\(,\\)(逗點)時
我們都是在這個表的最尾端加入一個資訊
現在
可以正式介紹\\((var)\\)了：

$$
(var) \quad \dfrac{\Gamma \vdash T: \star}{\Gamma, x: T \vdash x: T}
$$

舉個例子來說

$$
(var) \quad \dfrac{A: \star \vdash A: \star}{A: \star, x: A \vdash x: A}
$$

現在問題來了
如果變數不在語境的最尾端怎麼辦
舉例來說
要怎麼判決\\(A: \star, x: A, y: A \vdash x: A\\)？
\\((var)\\)規則只能作用在語境的最尾端
所以單靠這條規則是沒辦法得到以上判決的
因此我們需要另外2條規則

$$
\begin{array}{lcl}
(weak_1) & \dfrac{\Gamma \vdash x_1: T \qquad \Gamma \vdash U: \star}{\Gamma, x_2: U \vdash x_1: T} \\
(weak_2) & \dfrac{\Gamma \vdash x: T}{\Gamma, X: K \vdash x_1: T} \: \mbox{if } K是kind
\end{array}
$$

這2條規則告訴了我們
如果某個判決成立
則可以在該判決語境的尾端加入任何東西
判決依然會成立
如此一來
從\\(A: \star, x: A \vdash x: A\\)
就能推得\\(A: \star, x: A, y: A \vdash x: A\\)

還剩下5條規則 真累......

$$
\begin{array}{lcl}
(appl) & \dfrac{\Gamma \vdash t_1: T \to U \qquad \Gamma \vdash t_2: T}{\Gamma \vdash t_1 t_2: U} \\
(abst) & \dfrac{\Gamma, x: T \vdash t: U \qquad \Gamma \vdash T: \star}{\Gamma \vdash (\lambda x: T. t): T \to U} \\
(appl_2) & \dfrac{\Gamma \vdash t: \forall X: K. T \qquad U: K}{\Gamma \vdash t U: T[X := U]} \\
(abst_2) & \dfrac{\Gamma, X: K \vdash t: T}{\Gamma \vdash (\Lambda X: K. t): \forall X: K. T}
\end{array}
$$

和system F相比較
這4條規則幾乎完全沒變
我就不再度解釋它們了

$$
(conv) \quad \dfrac{\Gamma \vdash t: T \qquad \Gamma \vdash U: \star}{\Gamma \vdash t: U} \: \mbox{if } T \cong U
$$

這是最後一條規則
要是沒有這條規則的話
則沒有term的type會是\\((\lambda A: \star. A) B\\)
因為上面沒有一條規則產出的型別是type層級上的函數
但我們*確實*希望當\\(x: B\\)時
\\(x: (\lambda A: \star. A) B\\)

這條規則基本上告訴我們
要是\\(T\\)等於\\(U\\)而且\\(t: T\\)
則\\(t: U\\)
就直覺上
這是很好理解的
不過我們事實上碰到了一個大問題：
如何判斷兩個型別相等
這邊要採取一個簡單、常見又合理的選擇
我們用\\(\beta\\)-等價性來定義相等
至於什麼是\\(\beta\\)-等價性呢......
呃
我會從更簡單的等價性開始說起
最後再解釋\\(\beta\\)-等價性
先給個簡單的例子
\\((\lambda A: \star. A) B =\_\beta B\\)
這麼一來你應該能大概抓到\\(\beta\\)-等價(也就是\\(=_\beta\\))到底是什麼

首先介紹最簡單的等價性是什麼
這純粹就只是字面上的等價而已
它們的結構、變數名稱必須完全一樣
我把這樣的等價性寫作\\(=\\)
接下來介紹的等價性會建立在這之上

接下來是\\(\alpha\\)-等價性
在\\(\alpha\\)-等價性下
我們可以更改綁定變數的名稱
舉例來說
\\(\lambda x. xz =\_\alpha \lambda y. yz\\)
要更嚴謹地定義\\(=_\alpha\\)的話
這邊附上定義

$$
\begin{array}{lcl}
\lambda x. t =_\alpha \lambda y. t[x:=y] \\
如果t_1 =_\alpha t_2 則 \begin{cases}
                        t_1 t_3 =_\alpha t_2 t_3 \\
                        t_3 t_1 =_\alpha t_3 t_2 \\
                        \lambda x. t_1 =_\alpha \lambda x. t_2 \\
                        \end{cases}
\end{array}
$$

簡單來說2個term是\\(\alpha\\)-等價代表從其中一個term開始在任何地方更改綁定變數數次能得到另一個term
接著介紹\\(\beta\\)-等價
\\(T_1 =\_\beta T_2\\)代表的是\\(T_1\\)的NF\\(=\_\alpha T_2\\)的NF
換句話說
我們會盡量化簡等號兩邊的term
也就是說
如果對兩邊的term進行多次\\(\beta\\)-歸約
最終得到的結果會幾乎是同一個term
頂多只是綁定變數名稱不同而已
因為STLC是強規範化的
因此對\\(=_\beta\\)兩邊求NF的過程也一定會結束
不會遇到無窮迴圈
而這也就是我們想要的

回到\\((conv)\\)上頭
這條規則的前提有\\(\Gamma \vdash U: \star\\)
為什麼要有這個前提呢？
其實是因為技術上來說
一個合法的type可以\\(\beta\\)-等價於一個不合法的type
所以我們要有這個前提
