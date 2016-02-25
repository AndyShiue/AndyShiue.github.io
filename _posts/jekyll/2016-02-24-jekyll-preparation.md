---
layout: post
title: "Jekyll(1)"
categories: jekyll
---

我想把部落格轉移到Jekyll
為什麼用[Logdown](http://logdown.com/)撰寫文章不好呢？
原因有二：

1. Logdown對[Mathjax](https://www.mathjax.org/)的支援不甚理想
   不管在手機上還是電腦上
   數學式子都會出現奇怪的邊邊
   尤其在某些佈景主題下更是完全無法閱讀

2. 我希望讀者能夠更積極地參與撰寫教學的過程
   Logdown顧名思義就是個部落格
   這種類似[Wiki](https://www.mathjax.org/)的想法不是也不應該是它的設計理念

<!--more-->

此外我還對要轉移至的平台有著以下訴求

1. 能用[GitHub Flavored Markdown(GFM)](https://guides.github.com/features/mastering-markdown/)撰寫文章
   我覺得這是撰寫文章的一個很好的標記語言
   無論對於人類抑或是機器
   GFM都是高度可讀的

2. 和[Git](https://git-scm.com/)有著緊密連結
   我希望讀者能隨時提交Pull Request(PR)
   這使得文章的撰寫不再是單人的獨立活動
   而能成為所有人都能參與的共同活動

3. 能提供[Disqus](https://disqus.com/)的留言功能
   這麼一來
   即使是不會用/不想提交PR的讀者
   也能用留言進行簡單的互動
   例如問問題之類的

在以上的大前提下
我找到了**Jekyll**

# 簡介

在[Jekyll的官方網站](http://jekyllrb.com/)上
對於它的介紹是這麼寫的

> **簡單**
> 安裝時不再需要資料庫、評論審查、或者麻煩的更新
> 你只需要*你的(文章)內容*
> **靜態**
> 可含有Markdown(或Textile), Liquid, HTML和CSS
> 能直接佈署靜態網頁
> **適用部落格的**
> 永久連結、類別、頁面、貼文和自訂介面在這之中都是一級成員

哇！聽起來很棒！
而且[GitHub Pages](https://pages.github.com/)是直接基於Jekyll上
它當然是免費的
而且還和GitHub有著緊密的連結
來看看[怎麼](https://pages.github.com/)用Github Pages建立一個網站

# 建立網站

1. 首先
   [建立一個GitHub的repo](https://github.com/new)
   repo的名稱必須是*username*.github.io
   其中username是你GitHub上的使用者名稱(或機構名稱)
   啊對了
   我的使用者名稱是AndyShiue
   以下都將以AndyShiue做為例子

2. 如果沒有安裝Git的話
   請安裝它
   在[這裡](https://git-scm.com/downloads)你可以下載到Git
   下載後安裝應該是很簡單的事情
   之後請用`cd`移到你想要儲存檔案的資料夾
   以我來說的話
   是`C:\AndyShiue`
   所以請打開命令提示字元
   送出`cd C:\AndyShiue\`
   然後把你的repo複製下來
   `git clone https://github.com/AndyShiue/AndyShiue.github.io`

3. 然後進入你repo的資料夾中
   `cd AndyShiue.github.io`
   加入一個檔案`index.html`：
   `echo "Hello World" > index.html`

4. 接著把你本機的檔案推送到Github上
   `git add --all`
   `git commit -m "Initial commit"`
   `git push -u origin master`
   輸入帳號密碼 完成！

5. 完成了
   到http://Andyshiue.github.io
   你應該就能看到你的網頁
   如果進到你的網站是404的話
   那可能是因為你的GitHub帳號的email沒有驗證過

# 安裝

接下來介紹如何使用Jekyll
首先[在電腦上安裝Jekyll](https://help.github.com/articles/setting-up-your-pages-site-locally-with-jekyll/)
這樣你就能在推送網站到GitHub前先看看有沒有出什麼錯誤

1. 因為Jekyll是用[Ruby](https://www.ruby-lang.org/)寫的
   所以我們必須先[安裝Ruby](https://www.ruby-lang.org/zh_tw/documentation/installation/)
   如果你是Windows使用者
   可以下載並安裝[RubyInstaller](http://rubyinstaller.org/)
   如果你在之前沒有安裝過Ruby
   請重新啟動你的命令提示字元

2. 安裝[Bundler](http://bundler.io/)
   輸入`gem install bundler`

3. 輸入`gem install jekyll`
   恭喜你成功在你的電腦上安裝Jekyll了！

接著要安裝[Github Pages Gem](https://rubygems.org/gems/github-pages/versions/49)

1. 先移到你本來本機裡存放Github Pages的資料夾
   以我來說的話是`C:\AndyShiue\AndyShiue.github.io`
   
2. 在那個資料夾裡建立一個檔案`Gemfile`
   打開它並加入以下文字之後儲存檔案
```
source 'https://rubygems.org'
gem 'github-pages'
```

3. 在命令提示字元中運行`bundle exec jekyll build --safe`
   要是命令提示字元中有任何指示
   跟著它的指示做
   以我來說的話
   它會叫我運行`bundle install`
   然後又叫我跟著[這裡](http://github.com/oneclick/rubyinstaller/wiki/Development-Kit)的指示做
   我必須到[這裡](http://rubyinstaller.org/downloads/)安裝DevKit
   我把DevKit解壓縮在`C:\DevKit`
   然後`cd C:\DevKit`
   執行`ruby dk.rb init`
   開始安裝`ruby dk.rb install`
   安裝好了
   回到原本的資料夾`cd C:\AndyShiue\AndyShiue.github.io`
   再度執行`bundle install`
   等了好久......終於成功了！
   `bundle exec jekyll build --safe` 成功
   安裝好Github Pages Gem了
   現在你可以輸入`jekyll serve`預覽你的網頁
   天啊......又跳錯誤訊息了XDDDDDD
   它叫我安裝[kramdown](http://kramdown.gettalong.org/installation.html)
   [這邊](http://kramdown.gettalong.org/installation.html)叫我運行`gem install kramdown`
   再來一次 `jekyll serve`
   還是失敗......
   Google了一下
   輸入`bundle exec Jekyll serve`
   成功！
   在瀏覽器的網址列裡面輸入`http://127.0.0.1:4000/`就能看到你的網頁了