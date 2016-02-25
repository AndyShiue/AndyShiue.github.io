---
layout: post
title: "Jekyll(5)"
categories: jekyll
---

在這篇文章裡面
我想要進行幾件事情

1. 以目前來說
   如果你前置物設定了`title: "{{ page.title | escape }}"`
   那麼你文章的標題就會是`{{ page.title | escape }}`
   我覺得這不太好
   應該也要顯示我的網站名稱才對
   例如像這樣：`{{ site.title | escape }} - {{ page.title | escape }}`

2. 我想為文章提供Mathjax的功能
   我在上一個部落格中大量用到Mathjax
   要把那些文章移過來的話
   我必須要有Mathjax功能

3. 我想幫網站添加一個計數器
   記錄多少人來過這邊

來進行第1項吧
還記得上一次我們找到的`_layouts.default.html`嗎？
重新來看看它的原始碼：

```html
{% raw %}
<!DOCTYPE html>
<html>

  {% include head.html %}

  <body>

    {% include header.html %}

    <div class="page-content">
      <div class="wrapper">
        {{ content }}
      </div>
    </div>

    {% include footer.html %}

  </body>

</html>
{% endraw %}
```

可以發現到它把`<body>`之前的資訊都存放在`head.html`中
因此現在應該去看看`_includes\head.html`
原始碼如下：

```html
{% raw %}
<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">

  <title>{% if page.title %}{{ page.title | escape }}{% else %}{{ site.title | escape }}{% endif %}</title>
  <meta name="description" content="{% if page.excerpt %}{{ page.excerpt | strip_html | strip_newlines | truncate: 160 }}{% else %}{{ site.description }}{% endif %}">

  <link rel="stylesheet" href="{{ "/css/main.css" | prepend: site.baseurl }}">
  <link rel="canonical" href="{{ page.url | replace:'index.html','' | prepend: site.baseurl | prepend: site.url }}">
  <link rel="alternate" type="application/rss+xml" title="{{ site.title }}" href="{{ "/feed.xml" | prepend: site.baseurl | prepend: site.url }}">
</head>
{% endraw %}
```

你可以看到它儲存了`<head>`內的資訊
尤其是我們最關注的`<title>`
`<title>`內的東西如下：

{% raw %}
```html
{% if page.title %}{{ page.title | escape }}{% else %}{{ site.title | escape }}{% endif %}
```
{% endraw %}

這是一段Liquid程式碼！
可以大概看出來
意思應該是這樣的
如果`page`的`title`怎樣怎樣
那我們的標題就是`escape`後的`page.title`
否則標題是`site.title`
我稍微改一下
這樣在看文章的時候就也能看到`site.title`啦：

{% raw %}
```html
{% if page.title %}{{ site.title | escape }} - {{ page.title | escape }}{% else %}{{ site.title | escape }}{% endif %}
```
{% endraw %}

這麼一來
我們的第1點就完成了
第二點是讓網站支援Mathjax
Google搜尋"Jekyll Mathjax"
我們能找到[這個網頁](http://jekyllrb.com/docs/extras/)
它告訴我們加入這行程式碼：

```html
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
```

此外從[Mathjax的官網](https://www.mathjax.org/)
我找到了[它介紹的方法](http://docs.mathjax.org/en/latest/start.html#using-the-mathjax-content-delivery-network-cdn)：
加入以下程式碼：

```html
<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
```

我是不清楚有沒有`async`有沒有差別啦
不過有`async`好像比較帥的樣子
問題是這段程式碼要被放在哪裡？
我Google了"html script placement"
[這邊](http://stackoverflow.com/a/24070373/2128597)告訴了我答案
只要我的`<script>`是`async`的
我就可以直接把它擺在`<head>`裡面
所以就這麼做吧！

來試試看一段Mathjax吧：

$$ \sum_{n=1}^{\infty}\frac{1}{n^2}=\frac{\pi^2}{6} $$

成功了:DDDDDDDDD
接下來我要幫網站添加一個計數器：
Google "website counter"
我找到了[StatCounter](https://statcounter.com/)
我應該已經申請過它的會員了
讓我試試看登入...
失敗 還是申請一個新帳號好了
註冊後照著它說的設定做......

等等
我後悔了
我Google搜尋"website counter countries"後
找到了[Flag Counter](https://www.flagcounter.com/)
這個還可以顯示國家
所以來弄個counter吧
做好了！
它給我的程式碼如下：

```html
<a href="http://info.flagcounter.com/M8L4"><img src="http://s01.flagcounter.com/count/M8L4/bg_FFFFFF/txt_000000/border_CCCCCC/columns_8/maxflags_24/viewers_0/labels_0/pageviews_1/flags_0/percent_0/" alt="Flag Counter" border="0"></a>
```

我把它放在網站的最底下吧
編輯了一下`_includes\footer.html`
......似乎是搞定了
那這篇文章就這樣囉！
