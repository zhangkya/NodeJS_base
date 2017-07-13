##第1章 Node.js介绍
>在本章中你将学到：
>* Node.js是什么，为什么要创建它；
>* 使用Node.js能创建的应用程序示例；
>* 创建并运行第一个Node.js程序。

###1.1 什么是Node.js
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;为了能够更容易地编写出快速的、支持许多用户并且高效地使用内存的联网软件，Ryan Dahl创建了Node.js。<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在Ryan Dahl探索解决该问题方法的同时，Google工程师给Chrome浏览器编写了javascript引擎，它是专门为Web而设计的经过高度优化的软件。Google希望V8能够发扬光大，于是将其以BSD协议开源。<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Ryan Dahl决定使用V8引擎来创建javascript服务器端环境，这样做具有如下理由。
* V8引擎极快
* V8专注于WEB，所以在处理超文本传输协议HTTP、域名系统DNS和传输控制协议TCP等事务上架轻就熟。
* javascript在Web上人尽皆知，所以大多数开发人员都能使用它。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;从核心上说，Node.js是个事件驱动的服务端javascript环境。也就是说，我们可以像使用PHP、Ruby和Python语言那样，使用javascript创建服务器端应用程序。对于网络以及创建与网络交互的软件它尤为专注。

###1.2 使用Node.js能做什么
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Node.js是个程序设计平台，只要有想法和足够的编程技艺，它就无所不能。它既可以创建对文件系统进行操作的小段脚本，也可创建大规模的Web应用程序来运行整个业务。由于Node.js的独特设计，它非常适合于多个游戏、实时系统、联网软件和具有上千个并发用户的应用程序。

以下是一些使用Node.js的公司
* LinkedIn
* eBay
* Yahoo！
* Microsoft

能使用Node.js创建的应用程序有：
* 实时多人游戏
* 基于WEB的聊天客户端
* 将网络中的数据源进行合并的混搭软件（Mashup）
* 单页面浏览器应用程序
* 基于JSON的API

><b>注意：什么是服务器端的Javascript？</b><br/>
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;大多数WEB开发人员都熟悉使用Javascript操纵浏览器中的Web页面并与之交互。这就是通常所称的客户端Javascript，因为它发生在浏览器或者客户端。服务器端Javascript发生在把页面发送给浏览器之前的服务器上，当然，使用的是同样的语言。

###1.3 安装并创建第一个Node.js程序
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;说得够多了！现在看看运行中的Node.js并编写你的第一个Node.js程序。首先得安装Node.js。用于Windows和OSX的安装程序可以在Node.js的主页下载：http://nodejs.org。要想在这此平台上安装Node.js，只需要下载相关文件并双击安装程序即可。如果使用Linux或者想手动编译Node.js，请在https://github.com/joyent/node/wiki/installation上找操作指南。
####1.3.1 验证Node.js正确安装
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;安装Node.js之后，应当验证其是否正确安装。我们需要使用终端来与Node.js交互。如果是在OSX下，可以在Applications-->Utilities-->Termanl找到终端应用程序。如果是在Windows下，可以通过按Win+R键，然后输入cmd来启动一个终端，在Linux下，终端应用程序通常称为Termiinal。
<hr/>
<b>TRY IT YOURSELF</b><br/>
使用如下步骤来检查Node.js是否成功安装。
1. 打开终端输入node
2. 你应当看到一个提示符
3. 输入1+1，可以看到系统返回2
<hr/>

####1.3.2 创建“Hello World”Node.js程序
现在创建一个能启动WEB服务器并显示Hello World的Node.js程序。<br/>
<b>创建并保存为server.js程序</b>

```nodejs
var http = require('http');
http.createServer(function (req,res) {
  res.writeHead(200,{'Content-Type':'text/plain'});
  res.end('Hello World\n');
  }).listen(3000,"127.0.0.1");
  console.log('Server running at http://127.0.0.1:3000/');
```

从终端运行这个程序：`node server.js`，可以看到Server running at http://127.0.0.1:3000/，在浏览器运行地址看到"Hello World!"

###1.4 小结
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;好极了！你刚刚创建并运行了第一个Node.js程序。虽然这只是一个简单的事例，但在将来的几章里你将可以创建出更为复杂的应用程序，包括一个聊天服务器和一个实时的Twitter客户端。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;除了创建一个简单的服务器以外，在本章我们还学到：Node.js运行在V8引擎之上，这是一个由Google开发的开源的Javascript引擎。我们还了解到Node.js有多种用途，且精于创建有上千个并发用户的联网应用程序。
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在随后的几章里，我们将探究Node.js与其他编程语言和框架的不同，尤其是那些让它运行神速的特性，还要探究编写代码来利用这些特性的方法。

###1.5 问与答
<b>问：我能在服务器上使用Javascript吗？JavaScript不是只能在浏览器上用吗？</b><br/>
<b>答：</b>JavaScript绝对可以用在服务器上，而且它的许多特性使其精于此道。编写服务器端的JavaScript有许多好处，尤其在需要处理并发的时候。如果读者有使用诸如jQuery这样的框架编写JavaScript的经验，就会在Node.js中看到相似的模式。

<b>问：创建Web应用程序，Node.js比PHP、Python、.Net或者Ruby好吗？</b><br/>
<b>答：</b>要评估哪个编程语言最好，就犹如试着说世界上哪个城市最好。这要看情况，要创建的应用程序类型决定你的选择。不过，可以这么说，Node.js能胜任其他编程语言胜任的大多数事情，并且精于其他语言和平台所不精的领域。

<b>问：是否需要对Node.js是个新不台而担心？</b><br/>
<b>答：</b>在编程方面，Node.js相对年轻。开发的速度正在加快，世界各地的开发人员每天都在创建新的库。使用Node.js的优势在于，可以访问一个顶尖的并且从其他编程语言中受益良多的平台。涉足Node.js社区，现在是最好的时候。

<b>问：为了使用Node.js，我是否需要是个javascript编程专家？</b><br/>
<b>答：</b>你需要使用JavaScript来编写Node.js应用程序，但完全没必要是个专家。JavaScript这个语言成功的原因之一就是它的可访问性。就其本质而言，Javascript是个简单的语言，所以无需且怯。此外，Node.js使用大量模式，你将很快熟悉它们。
