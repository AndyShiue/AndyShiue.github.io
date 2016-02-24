---
layout: post
title: "Jekyll(3)"
categories: jekyll
---

我決定重新來過
砍了整個repo
然後成立一個預設的新專案觀察一個Jekyll網站的架構

<!--more-->

```
jekyll new C:\AndyShiue\AndyShiue.github.io
```

然後一樣建立一個`Gemfile`

我發現我一開始就該這樣了
`jekyll new`似乎已經提供了一個極簡又可用的網站
根據官網[資料夾結構](https://jekyllrb.com/docs/structure/)的資料
我知道了資料夾中的`index.html`是網站的首頁
`_config.yml`記錄了網站最基本的設定
`_post`資料夾中則存放著一般的貼文
所有Jekyll的文件的最開頭似乎都要有一段YAML做為[前置物](https://jekyllrb.com/docs/frontmatter/)
前置物......簡單來說好像是紀錄了某些metadata就是了
如果真的沒有要提供任何資訊
只要在文章開頭輸入2行各3個減號：

```
---
---
```

總之
我先試著把[Jekyll(1)](http://pigggggggggggggy.logdown.com/posts/2016/02/24/546001)丟到`_post`裡面吧
並參考範例加入以下前置物：

```
---
layout: post
title: "Jekyll(1)"
categories: jekyll
---
```

試著在本機跑了一次
Markdown的部分有正確讀取到
問題是它並不是使用GFM
Google "Jekyll GFM"會查到官網的[調校](http://jekyllrb.com/docs/configuration/)頁面
我發現只要在`_config.yml`裡加入2行就能開啟GFM的功能
跟著做吧：

```
kramdown:
  input: GFM
```

太好了
一下就成功了
我決定編輯一下`_config.yml`的個人資料
順便把Jekyll的這幾篇教學移到Jekyll上
然後把整個網站推到Github上
今天就到此為止