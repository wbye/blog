##WEB前端 - “懒人”养成计划 - 1

### 何为懒？
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;懒在人一开始的印象中，总是给人一种不好的感觉，勤奋一直是传统美德，懒是坏东西。最近看过一篇关于懒人科技的文章，觉得很有道理，文章有如下部分：

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_人类历史上曾诞生了琳琅满目的懒人科技，不断迁就着人性的弱点，有汽车、火车、飞机这种大型地、颠覆式发明，也有一些非常酷炫的小型创意，甚至还诞生了不错的服务，事实上，整个第三产业的市场就是来源于“懒人不想做的事情”。这些创意在改变人类生活的同时，也改变了懒汉的定义，在拥有了大量的新鲜玩意之后，他们的境界正大有提高，事实上，懒已经不是完全意义上的贬义词，在一定程度上，代表着高逼格。_


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;作为一名码农，更作为一名页面仔，我只想说：哪一个程序员，不想在写代码的时候偷点懒？当然这个懒，不是指那种当个纯粹的搬运工（CTRL+C,CTRL+V大神）。正是为了更“懒”，更愉快，更爽，更有逼格的写代码，才有了这篇文章。


###先看下前端现状
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_由于近几年前端的野蛮生长以及前端应用的多元化和复杂化，整个技术形态已经跟几年前纯做页面的时代完全迥异了。主要观念的变化总结来看在于一点，现在的前端开发面向的是web app而不是web page。前端如今已经脱离了茹毛饮血、刀耕火种的原始社会，开始步入了工业时代。_ 感谢这个快速发展的环境，给了页面狗，一个偷懒的机会：依靠新工具，新技术，极大的提高生产力。

###工欲善其事，必先利其器
一个标准页面仔的日常，应该是这样子：写写HTML，调调CSS，然后调试JS，然后页面搞定（送去给测试，发现IE bug ，哈哈）。说实话，写这个无聊的HTML，CSS，能把人写吐，或许你需要这个：

![EMMET](http://7xs3q2.com1.z0.glb.clouddn.com/record.gif)


还有这样：

![EMMET](http://7xs3q2.com1.z0.glb.clouddn.com/new-record-2.gif)

EMMET：前端神器，页面仔必备啊！

EMMET具体使用及下载，请参考[官网](http://docs.emmet.io/) http://docs.emmet.io/


###让CSS可编程，带你装逼带你飞

这年头，你要是出去面试，不知道LESS，SASS，PostCSS，你都不好意思说你是前端。可见LESS，SASS之流行。在我理解看来，一直把LESS，SASS还有其他的比如PostCSS看成一种工具，没当成语言来看待，就是为了让CSS可编程，更方便的去写CSS，更好的管理CSS，然后编译生成CSS。

当然，这篇文章不会讨论他们语法差异以及谁好谁坏，在我看来，适合自己的，适合项目的，就是好的。

[SASS十分钟入门](http://www.w3cplus.com/sassguide/)

SASS一瞥
![SASS一瞥](http://7xs3q2.com1.z0.glb.clouddn.com/C32DD61B-2E40-4723-99B6-9D8AFB08CEC0.png)


###快速创建前端静态网站 - http-server

一个命令就可以创建好一个http服务器，真是爽飞了

![http-server](http://7xs3q2.com1.z0.glb.clouddn.com/%E6%9C%AA%E6%A0%87%E9%A2%98-1.jpg)

[Github HttpServer](https://github.com/indexzero/http-server)


###自动化构建工具GULP - 串起你的整个项目

GULP是个基于流的构建工具，使用nodejs实现的，这对页面仔来说，简直太棒了。使用GULP，可以完成文件压缩，JS混淆，编译SASS，LESS 等，基本上你想要的功能，都可以通过代码实现。在项目，我还用GULP来下载文件，更新本地的JSON数据。主要解决了一个自己手动下载JSON数据的问题，都是为了偷懒。。。

有关具体GULP的介绍，请参考[GULP](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md)

###珍惜键盘，远离F5 - Browsersync

页面仔每天做的最多的事就是，刷新浏览器，F5 or CTRL+F5 ...

试想，当我写完HTML，CSS，JS 浏览就自动刷新，这真是飞一般的感觉。Browsersync给你想要的，甚至还他还内置了移动端调试神器WEINRE，简直不要太diao。

[Browsersync官网](https://www.browsersync.io)


### 光说不练假把式 - 手把手带你飞

STEP-1：准备好各种环境
	首先你得有nodejs环境，然后你得全局安装GULP，http-server,browsersync,如下所示：
	![DEMO](http://7xs3q2.com1.z0.glb.clouddn.com/npm-install-g-1.jpg)
	安装超时的同学，建议使用淘宝npm源，具体可见[CNPM](http://npm.taobao.org/)

STEP-2：克隆我事先写好的git懒人模板仓库
	git clone https://github.com/wbye/maybe_lazy_1.git
	![DEMO](http://7xs3q2.com1.z0.glb.clouddn.com/git-clone-lazy.jpg)
	
STEP-3：查看仓库README文件
	在终端运行： npm install
	![DEMO1](http://7xs3q2.com1.z0.glb.clouddn.com/cnpm-complete.jpg)
	完成后运行： npm run http-server ,  
	再另启个终端，运行： npm run bs-server
	![DEMO2](http://7xs3q2.com1.z0.glb.clouddn.com/record-3.gif)
	
STEP-4：体验一把做懒人的感觉O(∩_∩)O
	![DEMO1](http://7xs3q2.com1.z0.glb.clouddn.com/record-4.gif)

STEP-5: 懒人第一阶段完成，好了不写了，我要去好好板砖了
		
	




