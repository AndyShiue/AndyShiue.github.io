---
layout: post
title: "CTAGI (0 - A very short introduction)"
categories: lambda
---

新連載:D
先介紹一下這系列文章會出現的背景吧

一直以來
我都對程式有著不小的興趣
但與其說是對寫程式有興趣
倒不如說是喜歡更高層次的*抽象*
大家知道程式的規模越來越大時
就必須建立越高層次的抽象吧
為了不讓程式的複雜程度到一個人無法接受的程度

在這樣的背景下
我進入了FP的世界
其實最初是從[Scala](http://www.scala-lang.org/)開始
不過一下就跳進了[Haskell](https://www.haskell.org/)的坑
我首先閱讀了廣受好評的[LYAHFGG](https://www.gitbook.com/book/mno2/learnyouahaskell-zh/details)
雖然讀完LYAHFGG還不夠讓讀者真正有能力輕鬆的用Haskell寫程式
但它卻是非常容易閱讀的入門教材
後來會越多Haskell之後
當然就必須對它的各種extension有所了解
現在Haskell越來越往dependent types的方向發展
我當然也要跟上
後來變成跑去摸[Agda](http://wiki.portal.chalmers.se/agda/pmwiki.php)和[Idris](http://www.idris-lang.org/)
也學了一點lamdba calculus

然後
我碰到了[HoTT](http://homotopytypetheory.org/)
這似乎是另一套可以被當成數學基礎的理論
但......我發現如果不懂一些範疇論(category theory)
好像很難完整理解HoTT
所以我就來學範疇論囉
其實之前也常常看到一些Haskell方面的文章提到範疇論啦

我找到了好幾本範疇論的書
但都不甚理想(至少對我來說)
而目前為止最讓我滿意的就是這本啦
[Category Theory: A Gentle Introduction](http://www.logicmatters.net/resources/pdfs/GentleIntro.pdf)
我簡稱為CTAGI
這系列的文章會對書中的內容加以補充
對於數學基礎較差的人(例如我)來說應該會比較有用
我把我走過的路寫下來
這樣其他人就不用再重新費一番功夫

好了
進入書中吧
來看看目錄
一開始是第0章

> 0.1 Why categories?

簡單來說
數學是關於抽象的一門學科
例如像群
或是拓樸空間
就把某些性質用非常抽象的概念表達出來
我們接下來能把群或者是拓樸空間*之間*的概念再進行抽象
然後在那上頭再進行抽象......依此類推
而這就是範疇論在進行的事情
所以 呃 它很抽象

> 0.2 What do you need to bring to the party?

這節在說讀者需要的先備知識
這邊我要岔個題
提到programming中的[DRY原則](https://zh.wikipedia.org/wiki/%E4%B8%80%E6%AC%A1%E4%B8%94%E4%BB%85%E4%B8%80%E6%AC%A1)
DRY原則提到
要是你做了同一件事情兩次
你就應該把這兩次行為抽象掉變成一次
但反過來說
如果一個抽象沒有被使用兩次以上
那它就是過度設計
對應到了此節對於範疇論的觀點
如果你知道的數學不夠多
你就沒辦法理解為什麼要提供範疇論這樣的抽象
還好似乎你只要對那些數學有著最基本的認識就好了

> 0.3 Theorems as exercises

這本書沒有習題

> 0.4 Notation and terminology

都是很常見的慣例
直接讀書就好囉
