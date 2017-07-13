##第2章 npm（Node包管理器）
>在本章中你将学到：
>* 使用npm为Node.js安装模块；
>* 为Node.js的应用程序查找模块；
>* 在Node.js应用程序中使用模块；
>* 查找Node.js模块的文档；
>* 使用package.json文件。

###2.1 npm是什么

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;npm（Node Package Manager，Node包管理器）是Node.js的包管理器。它允许开发人员在Node.js应用程序中创建、共享并重用模块。它也可用于共享完整的Node.js应用程序。模块就是可以在不同项目中重用的代码库。如果你使用其他语言写过程序。那么npm就类似于Ruby中的RubyGems、Perl中的CPAN、Python中的pip或PHP中的PEAR

典形的模块示例包括：
> * 用于与数据库交互的库；
> * 验证输入数据的库；
> * 分析yaml文件的库。


<b>注意：大多数模块都是开源的</b>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Node.js社区在开源授权协议下发布了大多数模块。这也就意味着模块可以自由安装、修改和分发。

##2.2 安装npm

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;如果使用来自 http://nodejs.org 的安装程序安装了Node.js，那么npm就已经安装好了。如果从源代码安装编译了Node.js，那么可以在http://npmjs.org 找到npm的操作

##2.3 安装模块

安装了npm之后，就可以从终端开始安装模块了：
```
npm install [modeule_name]
```
这个命令向npm注册服务器发送请求，将某个模块的最新版本下载到计算机上

##2.4 使用模块

要在Node.js应用程序中使用模块，在下载它们之后必须请求（require）它们。在应用程序另请求一个模块的方法如下：
```
var module = require('module');
```
##2.5 如何找模块

既然可以安装Node.js模块，就会想探究有哪些模是可用的。Node.js有一个充满生机的开发者社区，模块的建立和维护每天都在发生

###2.5.1 官方来源

你可以在许多地方搜索模块。首先，在http://serch.npmjs.org 上有一个官方的基于WEB的npm搜索工具。这是寻找第三方模块的正统资源。

###2.5.2 非官方来源

还有许多非官方的来源可用于搜索npm模块。这些来源使用官方的注册数据，但在模块上增加了一些额外的信息。

Blagovest Dachev创建了http://blago.dachev.com/modules 站点，这个站点可以提供GitHub上某个项目的围观者数量、分叉（fork）数量以及问题数量

Eirik Brandtzag创建了一个类假的工具，地址是http://eirikb.github.com/nipster 它在Node.js社区也广受欢迎。它根据GitHub上的分叉数量对项目评级，而分叉数量是项目流行程序度的风向标

##2.6 本地和全局的安装

可以使用npm以两种方式安装模块，理解它们的工作方式很重要。

###2.6.1 本地安装

本地安装意味着库将安装在项目本地一个名为node_modules的文件夹下（在安装underscore库时就是如此）以便项目使用。这是默认行为，只要运行如下命令，就是如此：
```
npm install [module_name]
```
如果Node.js应用程序的名称是foo.js，这将产生如下的文件夹结构：
```
-foo.js
-node_modules/
  -modeule_name
```

这是最为常见的并且推荐的安装Node.js模块的方法

###2.6.2 全局安装

有些模块带有可执行文件，你希望能够在文件系统的任何一个位置都能运行这些可执行文件。Express就是一个可能需要全局安装的模块示例。Express是Node.js的一个Web开发框架，带有一个能够创建站点骨架的生成器。

要全局安装模块，只需在安装时加上-g标记
```
npm install -g express
```
全局安装一个模块意味着可以在文件系统的任何位置运行它。


##2.7 如何找模块文档

知道如何安装与寻找模块之后，我们还需要知道它如何使用它们。通常来讲，Node.js模块都有编写良好的文档，可以通过运行如下的命令在浏览器中查看模块文件：
```
npm docs [modeule_name]
```
这会打开浏览器并进入模块作者所提供的文档页面。这通常是一个指向GitHub上某个README文件的链接。要查看underscore.js文档，请运行：
```
npm docs underscore
```
通过运行如下命令也可以查看项目的bug
```
npm bugs underscore
```
这会打开浏览器并进入模块作者所提供的问题页面。随着经验的提升，就会发现阅讯模块源代码是理解其作用的最快方法
```
npm edit underscore
```
这里有个意外，那就是这个命令必须在Node.js项目文件夹的根目录下运行，而且该模块必须已经下载到了node_modules文件夹中。

##2.8 使用package.json指定依赖关系（dependency）

在开发Node.js应用程序的时候，毫无疑问要使用模块。一个一个地安装模块会是件耗时的工作，而且容易出错，比如，要是忘了安装某个模块怎么办？

不必担心npm允许开发人员使用package.json文件来指定在应用程序中要用的模块，并且通过单个命令来安装它们
```
npm install
```
这样做具有如下优势：
+ 无需一个一个地安装模块
+ 其它开发人员可以很容易地安装你的应用程序
+ 应用程序的依赖关系储存在单一的地方。

回到underscore模块那个例子上。现在可以给项目添加一个package.json文件。文件仅包含以特定格式表示的项目信息。一个最小的package.json文件会是这样的：
```
{
  "name":"example02",
  "version":"0.0.1",
  "dependencies":{
    "underscore":"~1.2.1"
  }
}
```

##2.9 小结

在本章中，我们学习了如何安装Node.js的包管理器npm。此外也学习了如何使用npm安装模块以及如何在Node.js应用程序中使用它们。我们学习了本地安装模块和全局安装模块的区别，以及如何寻找模块文档。最后，我们学习了如何使用package.json来声明应用程序中的依赖关系。

##2.10 问与答

**问：我刚刚开始学习使用NOde.js，我应当使用模块吗？**<br/>
<b>答：</b>是的。通过使用模块可以快速地给应用程序加入许多功能。模块通常可以为开发人员除去常见的困难。比如，Express模块可以让使用Node.js进行Web开发变的简单。

<b>问：有许多模块可以解决我的问题，哪个模块最好？</b><br/>
<b>答：</b>你应当使用社区中最为流行的模块。可以通过位于http://blago.dachev.com/modules 和 http://eirikb.github.com/nipster/ 的搜索工具来评估模的流行程度以。GitHub上围观者数量最能衡量流行程度

<b>问：我应该使用第三方模块还是自己编写代码？</b><br/>
<b>答：</b>编写自己的代码是理解问题的最好方式，但在许多时候，你的问题已经有人解决了，此时可以考虑在应用程序中使用第三方模块。许多开发人员最后还会为其使用模块修复bug并贡献新功能。
