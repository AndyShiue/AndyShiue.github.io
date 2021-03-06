---
layout: post
title: "CTAGI (1.1 - The very idea of a category)"
categories: CTAGI
---

> 1.1 The very idea of a category

看到了第1章
這章節正式介紹了何謂**範疇(category)**
範疇是啥呢？
一個範疇包含了兩種**資料(data)**
一是**物件(object)**
二是**箭頭(arrow)**
箭頭的頭被稱為**目標(target)**
尾則被稱為**源頭(source)**
每個箭頭的目標和源頭都必須分別是一個特定物件
之後一個箭頭會被寫成\\(f: A \to B\\)或\\(A \overset{f}{\rightarrow} B\\)
代表著\\(f\\)是源頭為\\(A\\)且目標為\\(B\\)的箭頭
而且對於任意兩個箭頭\\(f\\)和\\(g\\)
存在他們的**複合(composition)**
寫作\\(g \circ f\\)
這個用圖會比較清楚
假設有3個物件\\(A, B, C\\)
\\(A \overset{f}{\to} B \overset{g}{\to} C\\)
那麼一定可以找到一個\\(A\\)到\\(C\\)的箭頭
寫作\\(g \circ f\\)

這邊要特別澄清一點
假設\\(A \overset{f}{\to} B \overset{g}{\to} C\\)
你想要有一個\\(A \to C\\)的箭頭
你可能會想著*先*從\\(A\\)走到\\(B\\)*再*從\\(B\\)走到\\(C\\)
所以寫成\\(f \circ g\\)
但這是不對的
為什麼？
因為箭頭在很多範疇中都代表著*函數*
在那樣的狀況下
源頭就是函數的定義域
目標則是對應域
事實上
上面用的符號和函數符號是一樣的
假設我們有\\(f: A \to B\\)和\\(g: B \to C\\)
函數的複合被定義成\\(g(f(x))\\)
寫成\\((g \circ f)(x)\\)在這樣的狀況下便是很自然的方式了
值得一提的是
箭頭不一定要是函數
在範疇論的世界裡
連函數的概念都被抽象掉了

除此之外
一個範疇還必須滿足以下這些額外條件：

1. 箭頭滿足*結合律(associativity)*
   也就是說
   \\(h \circ (g \circ f) = (h \circ g) \circ f\\)
   用白話文說
   *複合的執行順序並不重要*
   因此之後大可把\\(h \circ (g \circ f)\\)或\\((h \circ g) \circ f\\)寫成\\(h \circ g \circ f\\)(省略括號)

2. 每個物件都存在從自己指向自己的箭頭
   稱為**identity**
   \\(A\\)的identity寫作\\(1_A\\)

1.1節就到此結束
