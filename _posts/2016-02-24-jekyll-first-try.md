---
layout: post
title: "Jekyll(2)"
categories: jekyll
---

看了一下
Jekyll實在很複雜
看起來是滿通用的一套架構
但也因為如此不好理解
我想先套用[Jekyll Bootstrap](http://jekyllbootstrap.com/)
之後再慢慢修改它的程式碼使其符合自己需要
首先刪除掉原有repo的所有檔案
在命令提示字元中輸入
```
git clone https://github.com/plusjade/jekyll-bootstrap.git AndyShiue.github.io
cd AndyShiue.github.io
git remote set-url origin git@github.com:AndyShiue/AndyShiue.github.io.git
git push --force origin master
```
注意我事實上修改了一些部分
原本命令中的所有`com`都被我改成了`io`
另外push後面加了參數`--force`
這樣才對

然後
似乎這樣就好了？
我試著建立一篇自己的文章
我把[Jekyll(1)](http://pigggggggggggggy.logdown.com/posts/2016/02/24/546001)這篇文章丟進`C:\AndyShiue\AndyShiue.github.io\_posts\`
開頭參考Jekyll Bootstrap提供的範例加上一些資訊

```
---
layout: post
category : jekyll
tags : [jekyll, tutorial]
---
{% raw %}
{% include JB/setup %}
{% endraw %}
```

然後試著執行`bundle exec Jekyll serve`看看有沒有成功加入一篇新文章
等等 它告訴我我之前的`Gemfile`不見了
所以我要重創一個
再度執行`bundle exec Jekyll serve`
結果是所有的CSS都沒載入
我決定整個砍掉重練
從基本功開始學起