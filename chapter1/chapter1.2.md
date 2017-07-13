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
