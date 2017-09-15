---
layout: post
title: "Jekyll(4)"
categories: jekyll
---

這次來仔細看看Jekyll的[資料夾結構](https://jekyllrb.com/docs/structure/)吧

1. `_config.yml`
   這個是整體的設定
   檔案格式是YAML

2. `_drafts`
   這是儲存草稿的資料夾
   資料夾內的檔案必須以`title.MARKUP`命名
   其中`MARKUP`是檔案的附檔名
   例如像Markdown就是md之類的

3. `_includes`
   這資料夾底下的檔案的用途應該在於
   假如一段字串在網頁裡的各個部分出現很多次
   那麼就應該把這些資訊提取出來
   存在這個資料夾內
   `{% include file.ext %}`可以把字串從`_includes/file.ext`貼上

4. `_layouts`
   這個資料夾內儲存的是網頁的排版方式
   要怎麼更改排版方式呢
   只要在你的網頁的前置物中加上`layout: XXX`
   網頁就會依照`_layouts\XXX.html`的格式排版了

5. `_posts`
   這是你貼文儲存的地方
   裡面檔案的檔名格式會是`YEAR-MONTH-DAY-title.MARKUP`
   舉例來說像本文的檔名是`2016-02-25-jekyll-directories.md`

6. `_data`
   儲存資料的地方
   裡面的資料一樣要有前置物
   格式可以是`.yml`, `.yaml`, `.json` or `.csv`

7. `_site`
   這是儲存生成的網站的地方
   Jekyll似乎會把所有那些亂七八糟的檔案格式(`.yml`, `.md`, `.html`... etc.)轉換成真正的網頁存到這裡面
   請設定`.gitignore`以忽視掉這個資料夾

8. `.jekyll-metadata`
   顧名思義
   儲存metadata的地方
   看來我們一般使用者不太需要管它
   官方網站叫我們也把它加入`.gitignore`

9. 其它有YAML前置物的檔案
   一律會被經由Jekyll處理

10. 其它
    例如像CSS, 圖片之類的
    會被原封不動地加入生成的網站中

我已經很清楚`_config.yml`和`_post`是做什麼的了
接著來看看`_layouts`吧

```html

---
layout: default
---
<article class="post" itemscope itemtype="http://schema.org/BlogPosting">

  <header class="post-header">
    <h1 class="post-title" itemprop="name headline">{{ page.title }}</h1>
    <p class="post-meta"><time datetime="{{ page.date | date_to_xmlschema }}" itemprop="datePublished">{{ page.date | date: "%b %-d, %Y" }}</time>{% if page.author %} • <span itemprop="author" itemscope itemtype="http://schema.org/Person"><span itemprop="name">{{ page.author }}</span></span>{% endif %}</p>
  </header>

  <div class="post-content" itemprop="articleBody">
    {{ content }}
  </div>

</article>

```

上面這是`_layout\post.html`的程式碼
雖然我不熟HTML
還是來慢慢讀

```yaml
---
layout: default
---
```

這個layout的最上面又設定了layout.....
那來看看`_layout\post.html`好了

```html

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

```

好了
這個應該真的是最基礎的layout了
你可以看到就是每個網頁都要用的東西
不過還滿細心的
為了進行抽象
還把head, header, footer都抽出來放在別的地方
但你仔細想想
為啥會有這些`{% %}`和`{{ }}`呢？
事實上
上面的檔案並不是真正的HTML
真正的HTML其實也不會有前置物啦XD
而是***真正的HTML**的模板*
這些模板由一個稱為Liquid的語言寫成
Liquid在經由Jekyll處理過後會生成真正的檔案
舉例來說`{% include XXX.html %}`這個Liquid的指令會去`_includes/XXX.html`把裡面的內容貼上到網頁裡面
還有`{{ content }}`代表了真正的內文
如果你在一個文件的開頭設定了`layout: default`
輸出的文件會是原本的文件嵌入在layout模板中的`{{ content }}`裡

這篇文章介紹了Liquid的基礎
就到這邊為止了喔！
