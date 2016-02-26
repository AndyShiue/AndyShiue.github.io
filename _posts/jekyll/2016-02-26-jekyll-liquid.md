---
layout: post
title: "Jekyll(6)"
categories: jekyll
---

{% raw %}

上次看到了一些Liquid的程式碼
這次我要更深刻地理解Liquid程式碼的意思
首先
我找到了[Liquid的官方網站](http://liquidmarkup.org/)
點旁邊的*文件*連結
到了[這個頁面](https://github.com/Shopify/liquid/wiki)
然後進到[Liquid for Designers](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers)

來讀一讀吧
我邊讀邊翻譯成中文

Liquid有兩種語言結構：Output和Tag
Output寫成`{{ XXX }}`
Tag寫成`{% XXX %}`

Output的例子有這些：

```
Hello {{name}}
Hello {{user.name}}
Hello {{ 'tobi' }}
```

除此之外Output還能加上filter
可以想成是作用於內容字串上的函數

```
Hello {{ 'tobi' | upcase }}
Hello tobi has {{ 'tobi' | size }} letters!
Hello {{ '*tobi*' | textilize | upcase }}
Hello {{ 'now' | date: "%Y %h" }}
```

接著網站上提供了很多內建的filter
我在這邊直接省略掉
沒記錯的話Jekyll也提供了一些它定義的filter

接著是Tag
Tag代表著某些程式邏輯
底下介紹了一些基本的Tag
例如像`{% comment %}`
被包圍在`{% comment %}`裡面的文字會被轉換成註解：

```
We made 1 million dollars {% comment %} in losses {% endcomment %} this year
```

還有`raw`
`raw`會把被包在裡面的文字原封不動的輸出
不會去處理裡面的指令
抱歉我無法提供範例
因為本篇文章就是用Jekyll寫的;P

然後Liquid還有一些控制結構
像`if`和`else`：

```
{% if user.name == 'tobi' %}
  Hello tobi
{% elsif user.name == 'bob' %}
  Hello bob
{% endif %}
```

網站上還提供了很多其它範例
還有`case`
這和C裡面的`case`類似：

```
{% case template %}

{% when 'label' %}
     // {{ label.title }}
{% when 'product' %}
     // {{ product.vendor | link_to_vendor }} / {{ product.title }}
{% else %}
     // {{page_title}}
{% endcase %}
```

當然也有迴圈和變數宣告
我懶得再翻譯了

這篇文章如果只有這樣好像有點短
所以我現在想要再幫每篇文章的底下加上Disqus的留言功能
Google "Jekyll Disqus"
我找到了[這篇文章](https://help.disqus.com/customer/portal/articles/472138-jekyll-installation-instructions)
基本上它是叫我在文章的開頭都加入一個`comments: true`的設定
然後檢查文章開頭有沒有`comments: true`
如果有的話就提供留言板的功能
我想反過來做
預設每篇文章都有留言板
如果不想要有留言板
再手動把留言取消
所以我在我的`\_layouts\post.html`底下加入這一段程式碼：

```html
{% unless page.no_comments %}
  <div id="disqus_thread"></div>
  <script>
    var disqus_config = function () {
        this.page.url = "http://andyshiue.github.io/{{ page.url }}";
        this.page.identifier = "{{ page.id }}";
    };
    (function() {  // DON'T EDIT BELOW THIS LINE
        var d = document, s = d.createElement('script');

        s.src = '//andyshiue.disqus.com/embed.js';

        s.setAttribute('data-timestamp', +new Date());
        (d.head || d.body).appendChild(s);
    })();
  </script>
  <noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript" rel="nofollow">comments powered by Disqus.</a></noscript>
{% endunless %}
```

再試著加上Facebook的讚按鈕好了
Google "Facebook Like website"
找到[FB的教學頁面](https://developers.facebook.com/docs/plugins/like-button?locale=zh_TW)
一樣編輯`\_layouts`裡面的檔案就好囉

{% endraw %}
