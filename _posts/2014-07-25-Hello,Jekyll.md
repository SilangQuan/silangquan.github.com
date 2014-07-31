---
layout: post
title: "Hello,Jekyll"
description: ""
category: 技术
tags: [Jeklly,blog]
---
<center><img src="/assets/post_images/20140725/2.png" alt="github+jekyll"></center>

##提要
花了两周多的时间搭建了基于Github pages + Jekyll 的博客。虽然是折腾了一些，可定制的东西就太多了，主题，内容...下面是整个搭建的过程。

环境：Ubuntu 14.04 64bit

##在github上跑上Jekyll
git环境的配置可以参考这里：[Git/Github的使用并与Eclipse整合](http://blog.csdn.net/silangquan/article/details/8964007)
git配置好之后就可以参考这个[Jekyll QuickStart](http://jekyllbootstrap.com/usage/jekyll-quick-start.html)来安装Jekyll了。
如果一切正确的话，打开对应的网址应该能够看到解析正确的网页了。
<center><img src="/assets/post_images/20140725/3.png" alt="github+jekyll"></center>

##本地预览
当电脑无法联网的时候如果需要更新博客就需要在本地预览了。
```
gem install jekyll
cd 博客的git文件夹
jekyll serve --watch
```
报错：
Could not find a JavaScript runtime.
解决方法，终端运行：
{% highlight sh linenos%}
sudo apt-get install python-software-properties 
sudo add-apt-repository ppa:chris-lea/node.js 
sudo apt-get update 
sudo apt-get install nodejs 
{% endhighlight %}

再次运行
{% highlight sh linenos%}
jekyll serve --watch
{% endhighlight %}
--watch表示实时编译，一但发现有文件发生改动就进行重新编译。
启动正常！
打开浏览器，进http://localhost:4000/.
和之前看到的效果一样。

<!--more-->

##主题设计
jekyll自带有两个主题，网上也有很多很多jekyll的主题，比如[这些](http://jekyllthemes.org/)，但是我觉得并不是很好...
参考了云风的blog，byvoid的博客，西乔的九卦等博客自己鼓捣了两天，设计好了一个还算满意的主题。
接下来就是切图，写html，写css...

##遇到的一些问题
**markdown解析引擎**<br>
默认的markdown解析引擎会有问题，需要修改_config.yml,添加一行：
{% highlight sh linenos%}
markdown: rdiscount
{% endhighlight %}

**评论系统**<br>
用的disqus，感觉蛮简洁的。
直接去[官网](https://disqus.com/)注册，然后按照提示在post.html后面加上一段代码就可以了。

**摘要**<br>
网上有几种方法，我用的最实用的方法，在文章里面添加一行html注释
{% highlight html linenos%}
<!--more-->
{% endhighlight %}
主页上对应的代码是
{% highlight html linenos%}
{% raw %}
	{% if post.content contains '<!--more-->' %}
    	<div class="post_content"> {{ post.content | split:'<!--more-->' | first }}
    		<a class="read_all"  href="{{post.url}}">阅读全文&nbsp"{{post.title}}"</a>
    	</div>
	{% else %}
   	 	<div class="post_content">{{ post.content}}
   	 	</div>
	{% endif %}
{% endraw %}
{% endhighlight %}
**域名绑定**<br>
这个陈小浩同学给我推荐了一个国内的域名提供商，注册了silangquan.com，花费55软妹币/一年。
在本地代码库里新建名为CNAME文本文件，在Terminal中输入，以我的域名为例:silangquan.com
{% highlight sh linenos%}
echo 'silangquan.com' > CNAME
{% endhighlight %}
然后push
{% highlight sh linenos%}
git add CNAME
git commit -am "CNAME ADDED"
git push
{% endhighlight %}
在域名控制台添加一条DNS解析记录：
登陆域名管理，在域名解析中添加
-主机记录：@
-记录类型：A
-路线类型：默认
-记录值：204.232.175.78
-其他：默认

这样设置会得到github的warning

>GitHub Pages recently underwent some improvements (https://github.com/blog/1715-faster-more-awesome-github-pages) to make your site faster and more awesome, but we've noticed that silangquan.com isn't properly configured to take advantage of these new features...

至今未解决...

**写文章**<br>
所有文章都保存在根目录的`_posts`文件夹中。去[这里](https://www.zybuluo.com)用markdown写文章,然后导出markdown文件，重命名，格式是时间+标题.md,比如：`2014-07-25-Jekyll简介(译).md`，还要添加上yaml头，比如：
{% highlight html linenos%}
{% raw %}
---
layout: post
title: "Jekyll简介"
description: ""
category: 技术
tags: [Jeklly,翻译]
---
{% endraw %}
{% endhighlight %}

图片的处理比较麻烦，有人会选择其他的传图片的网站，我还是选择把图片放在github上。
手动在assets文件夹中创建post_images文件夹，按博客的月份创建文件夹，将图片文件放到里面，文章就可以用相对路径来引用对应的图片了。最后在上传文章的时候记得连同图片一起上传。

**代码高亮**<br>
Jekyll原生支持语法高亮工具Pygments。Pygments支持超过100种语言， 并且支持多种输出格式，比如HTML, RTF等等。
安装：
{% highlight sh linenos%}
sudo apt-get install python-pygments
sudo gem install pygments.rb
pygmentize -S native -f html > your/css/folder/pygments.css
{% endhighlight %}

生成的css就是高亮的主题。
在default.html中将其引入，当然要想和自己的主题看起来和谐一些，还是要修改css。
遇到一个问题就是liquid语法冲突，就是你如果在md文件中贴liquid语句会被解析掉..解决方式是加上raw标签，中间的内容将不会被解析。
{% highlight html linenos%}
{% raw %}
{% raw %}
...注意删掉中间的空格
{ % endraw %}
{% endraw %}
{% endhighlight %}


##搭建日记
最后附上算是开发日记的东西，仅当记录吧。
7.15
修改了menubar。
menu的顺序可以写死在defaut.html中
下一步
添加menubar样式
修改背景颜色。

7.17
全部重写css。
刚开始写。
估计要一天时间。

7.19
完成主框架的搭建和头header的css。
明天把index搞定。
不能无限制的拖了。

7。21
 断断xuxu，搞得也差不多。
需要作的

1.页面内容的css。
2.右边的导航。
3.高度自适应。

7.22
遭遇各种bug，
1.markdown不能翻译表格，公式；
2.自定义分页的bug。

要做
1.解决bug。
2.定义号style.css
3.添加右边的链接

7。23
将index.md扩展名改为html，一切正常了。

上传到git上，发现没法更新，可能bug了吧。。。

需要作的
1。主页的弹性高度；
2.posts页的css；
3。添加评论

7.24 & 7.25
1.主页基本完成。
2.post。html需要加Css
3.添加评论系统
4.完成其他小页面。
5.代码高亮。
6.添加点击阅读。。。。。

7.26
小修改下post.html。
需要在windows去公司慢慢调整页面。

7.27
购买了silangquan.com的域名，但要实名审核。需要等几天。
添加了一篇影评，搞了一篇jekyll简介。
添加了Equioments页面。

7.28
成功绑定域名。
修改了下css。

7.29
基本完成。添加了Diqus的评论系统。美化了css。

