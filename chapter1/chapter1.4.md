##第4章 回调（Callback）
>在本章中你将学到：
>* 回调是什么，它们在Javascript中如何使用；
>* Node.js中如何使用回调；
>* 同步和异步编程的区别；
>* 事件循环是什么

##4.1 什么是回调

如果读者熟悉jQuery，那么使用回调就可能是家常便饭。回调指的是将一个函数作为参数传递给另一个函数，并且通常在第一个函数完成后被调用。在下面的jQuery示例中，使用jQuery的hide()方法隐藏了一个段落标记。这个方法可以使用一个可选的回调函数作为参数。如果提供了回调函数作为参数，那么当段落隐藏完成后它就会被调用。这就让我们有可能在隐藏完成后做一些事情--在本例中，我们显示一个提示。
```
$('p').hide{'slow',function{}{
  alert("The paragraph is now hidden")
}};
```
不过，回调是可选的。如果不需要回调，可以这么写代码：
```
$('p').hide('slow');
```
比较两段代码示例，第一段加入了一个匿名函数作为第二个参数，，并且在第一个函数完成后被调用。在第二个示例中没有回调。由于Javascript中函数是第一类（first-class）对象，它们可以以这种方式作为参数传递到其他函数中。于是我们就可以编定这样的代码：执行A，并且在执行完B之后再执行A。为了演示编写带与不带回调的代码之间的区别，我们在浏览器中看两段jQuery示例。
```
<!doctype html>
<html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Callback Example</title>
  </head>
  <body>
    <h1>Callback Example</h1>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer ut augueet orcialiquam aliquam. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesquehabitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Etiamfermentun dictum convallis. In at diam et orci sodales sollicitudin. Sed viverra, orcisit amet faucibus condimentum, nibh augue consectetur ipsum, eutristique dolor diaminterdum tellus. Donec in diam nunc. Nulla sollicitudin elitsit amet neque elementum accursus nibh lobortis.</p>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js"></script>
    <script>
      $(function () {
        $('p').hide('slow');
        alert("The paragraph is now hidden");
        });
    </script>
  </body>
</html>
```
在这个示例中，提示框会在段落隐藏之前显示。这是因为Javascript在hide()方法执行之后直接执行alert，即使段落尚未隐藏好。

在上面的示例中，我们看到提示信息在段落隐藏之前显示。这是因为alert在段落完成隐藏之前被执行。对于使用回调来确保某件事情完成之后执行另一件事情，这是个绝好的示例。以下这个相同的示例使用的是回调。
```
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Callback Example</title>
  </head>
  <body>
    <h1>Callback Example</h1>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer ut augueet orcialiquam aliquam. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesquehabitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Etiamfermentun dictum convallis. In at diam et orci sodales sollicitudin. Sed viverra, orcisit amet faucibus condimentum, nibh augue consectetur ipsum, eutristique dolor diaminterdum tellus. Donec in diam nunc. Nulla sollicitudin elitsit amet neque elementum accursus nibh lobortis.</p>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js"></script>
    <script>
      $(function () {
        $('p').hide('slow',function(){
          alert("The paragraph is now hidden");
          });
        });
    </script>
  </body>
</html>
```
现在这个示例在段落隐藏之后显示提示，提示框正确地出现在事件发生之后而不是之前。

##4.2 剖析回调

我们已经看到了在jQuery中回调的效果，但在Javascript内部它是怎么工作的？这里要掌握的关键概念是：函数可以作为参数传递到另一个函数中，然后被调用。在下面的示例中，创建了一个名为haveBreakfast的函数，它带有两个参数：“food”和"drink"。第三个参数是“callback”，这个参数传递给它的回调函数。
```
function haveBreakfast(food,drink,callback) {
  console.log('Having breakfast of ' + food + ', ' + drink);
  if (callback && typeof(callback) === "function") {
    callback();
  }
}
```
要使用haveBreakfast函数，我们传递被吃的食物和被饮用的饮料两个变量（在这里是吐司和咖啡），传递一个参数作为第三个参数。这是个回调函数，将会在haveBreakfast()函数内被执行。
```
haveBreakfast('toast','coffee',function(){console.log('Finished breakfast. Time to go to work!');
});
```
这样的回调模式在Node.js中到处使用，所以要花一些时间来理解这里所发生的一切。在本例中，回调函数在haveBreakfast()函数完成后做了某些事情。确切地要做的事情定义在作为回调传递进来的函数中。在这里要显示去工作！运行这一脚本会显示如下输出：

Having breakfast of toast, coffee<br/>
Finished breakfast. Time to go to work!

##4.3 Node.js如何使用回调

Node.js到处使用回调，尤其在有I/O操作发生的地方。下面是一个在Node.js中使用filesystem模块从磁盘上读入文件内容的示例。
```
var fs = require('fs');
fs.readFile('somefile.txt','utf8',function(err,data){
  if(err) throw err;
  console.log(data);
  });
```
 以下是所发生的事情
 1. fs(fielsystem)模块被请求，以便在脚本中使用
 2. 将文件系统上的文件路径作为第一个参数提供给fs.readFile方法
 3. 第二个参数是uft8，表示文件的编码
 4. 将回调函数作为第三个参数提供给fs.readFile方法
 5. 回调函数的第一个参数是err，用于保存在读取文件时返回的错误
 6. 回调函数的第二个参数是data，用于保存读取文件所返回的数据
 7. 一旦文件被读取，回调就会被调用
 8. 如果err为真，那么就会抛出错误
 9. 如果err为假，那么来自文件的数据就可以使用
 10. 在本例中，数据会记录到控制台上

 读者将会看到在Node.js中以这种方式一次又一次地使用回调。另外一个示例是http模块。http模块使得开发人员可以创建http客户端和服务器。读者已经在Hello World服务器中看过了http模块。http模块中的http.get()方法可用来请求Web服务器获得响应数据以便使用。
 ```
 var http = require('http');
 http.get({host:'shapeshed.com'},function(res){
   console.log("Got response:" + res.statusCode);
   }).on('error',function(e){
     console.log("Got error:" + e.message);
     });
 ```
以下是这段代码的解释
1. 请求http模块，以便在脚本中使用。
2. 给http.get()方法提供两个参数
3. 第一个参数是选项对象。在本示例中，要求获取shapeshed.com的主页
4. 第二个参数是一个响应作为参数的回调函数
5. 当远程服务器返回响应是地，会触发回调函数
6. 在回调函数内记录响应状态吗，如果有错误的话可以记录下来

回调函数的调用发生在远程服务器发回响应之后而不是之前。这个示例基本上演示了Node.js想要做成的全部事情。由于这段代码必须进入网络来获取数据，所以就不可能确切知道什么时候数据能返回，甚至都不能确认数据会不会返回。尤其在从多个来源和多个网络中获取数据时，由于数据返回的时间的不可预测本质，要编写代码对此作出响应将是困难的。Node.js是对这一问题的响应，它以提供一个创建联网应用程序的平台为目标。回调是Node.js实现网编程的关键方法，因为回调让代码在其他事件发生的时候能够运行（在本例中，也就是数据从shapeshed.com返回的时候）。当事件发生时，我们称回调被“触发(fired)”，从而导至回调函数被调用。在以下的程序清单中，4个不同的I/O操作都在发生，它们都使用回调。
> 演示网络I/O和回调

```
var fs = require('fs'),
    http = require('http');

http.get({host:'shapeshed.com'},function(res){
  console.log("Got a response from shapeshed.com");
  }).on('error',function(e){
    console.log("There was an error from shapeshed.com");
    });

fs.readFile('file1.txt','utf8',function(err,data){
  if (err) throw err;
  console.log('File 1 read!');
  });

http.get({host:'www.bbc.co.uk'},function(res){
  console.log("Got a response from bbc.co.uk");
  }).on('error',function(e){
    console.log("There was an error from bbc.co.uk");
    });

fs.readFile('file2.txt','utf8',function(err,data){
  if (err) throw err;
  console.log('File 2 read!');
  });
```
当代码运行的时候，它做如下事情
1. 获取shapeshed.com的主页
2. 读取file1.txt的内容
3. 获取bbc.co.uk的主页
4. 读取file2.txt的内容

 看看这个示例，你能说出哪个操作会选返回吗？这样的猜测显然不错：从磁盘上读取的两个文件很可能会先返回，因为无需进入网络。但仅此而已，我们难以说出被读取的文件哪个会先返回，因为我们不知道文件的大小。至于对两个主页的获取，脚本要进入网络，而响应时间则依赖于许多难以预测的事情。Node.js进程在还有已经注册的回调尚未触发之前将不会退出。回调首先是负责解决不可预测的方法，它也是处理并发（或者说一次做超过一件事件）的高效方法。

 ##4.4 同步和异步代码

 Node.js运行在单一的进程中并且要求开发人员使用异步编码风格。在上一个示例中，我们看到4个操作如何通过回调模式异步执行。不过以异步方式编程并不是Node.js或者Javascript特有的。这是一种编程风格。

 同步的代码意味着每一次执行一个操作，在一个操作完成之前，代码的执行会被阻塞，无法移到下一个操作上。程序清单4.2演示的是阻塞代码，它演示两个使用Node.js进行的操作：获取一个Web页面并且从第三方API获取数据。这个示例模拟了这此花费很多时间的操作及其对代码执行的影响。请注意，这个示例中,sleep()函数只是模拟完成了这些操作所需的时间花销的手段。

 > 程序清单4.2  同步（或者阻塞）代码

 ```
 function sleep(milliseconds){
   var start = new Date().getTime();
   while ((new Date().getTime() - start) < milliseconds){
     }
 }

 function fetchPage() {
   console.log('fetching page');
   sleep(2000);
   console.log('data returned from requesting page');
 }

 function fetchApi(){
   console.log('fetching API');
   sleep(2000);
   console.log('data returned from the api');
 }

 fetchPage();
 fetchApi();
 ```
在这个示例中，fetchPage()函数模拟从Internet上获取一个页面，而fetchApi()函数模专从第三方API获取数据。它们并不获取实际的数据，而是演示当响应所需的时间是个未知量时使用同步编程风格会发生什么。当脚本运行时，fetchPage()函数会被调用，直到它返回之前，脚本的运行是被阻塞的。在fetchPage()函数返回之前，程序是不能移到fetchApi（）函数中的。这称为阻塞操作，因为这种风络的代码阻塞了进程的运行真到函数返回。一件事情在另外一件事情之后有效发生。

Node.js几乎不使用这种编码风格，而是异步地调用回调。程序清单4.3演示了同样的操作，但是使用了Node的异步风格。注意这个示例通过网络对某个Web Service进行了请求来模拟慢的响应效果，而没有使用模拟的sleep()函数。

> 程序清单4.3 异步（或非阻塞）代码

```
var http = require('http')

function fetchPage(){
  console.log('fetching page');
  http.get({host:'trafficjamapp.herokuapp.com',path:'/?delay=2000'},
    function(res){
      console.log('data retruned from requesting page');
    }).on('error',function(e){
        console.log("There was an error" + e);
      }
  );
}

function fetchApi(){
  console.log('fetching api');
  http.get({host:'trafficjamapp.herokuapp.com',path:'/?delay=2000'},
    function(res){
      console.log('data returned from the api');
    }).on('error',function(e){
      console.log('There waw an error' + e );
      });
}

fetchPage();
fetchApi();
```
运行这段代码，就不再等待fetchPage()函数返回了，fetchApi()函数随之立刻被调用。这是可能的，因为代码通过使用了回调，是非阻塞的了。一旦调用了，两个函数都会侦听远程服务器的返回，并以此触发回调函数。注意，这此函数的返回顺序是无法保证的，而是和网络有关。

通过在终端上运行这两个示例，我们可以清楚地了解这两种编码风格对运行的是什么以及什么时候运行的影响。Node.js对如何在网络和I/O操作中处理并发（或者一次做超过一件事件）有自己的做法，所推崇的是异步方式。

如果读者是Node.js和Javascript新手，可能会混淆异步、同步、阻塞和非阻塞这几个术语。这些术语在Node.js社区和文档中大量使用，所以理解它们就很重要了。

同步和阻塞这两个术语可互换使用，指的是代码的执行会在函数返回之前停止，就如在前面的示例 所看到的。如果某个操作阻塞，那么脚本就无法继续。对于最终用户而言，这就意味着他们必须得等待。

异步和非阻塞这个这两个术语也可以互换使用，指的是基于回调的、允许脚本并执行操作的方法。脚本无需等待某个操作的结果老能继续前进，因为操作结果会在事件发生时由回调来处理。使用异步方法，操作无需一个接一个地发生。

##4.5 事件循环

现在，读者可能会问，这些神奇的事情都是如何发生的？Node.js使用Javascript的事件循环来支持它所推崇的异步编程风格。这可能又是一个难以掌握的概念。基本上，事件循环使得系统可以将回调函数先保存起来，而后当事件在将来发生时再运行。这可以是数据库返回数据，也可以是Http请求返回数据。因为回调函数的执行被推迟到事件发生之后，于是就远需停止运行，控制流可以返回到Node运行时的环境，从而让其他事情发生。

事件循环不是Javascript特有的，只是这个语言精于此道。Javascript围绕着事件循环设计，作为在有人与Web页面交互时对浏览器中所发生的不同事件进行响应的方式。这包括诸如单击鼠标或滚动页面的某个部分的事件。事件循环对于基于浏览器的交互而言是个良好的选择。因为要预测这些事件何时发生时并不容易。Node.js将这一方法应用到了服务端的编程上，尤其在网络和I/O操作的上下文中。Node.js经常被当成一个网络编程的框架，因为它的调计旨在处理网络中数据流的不确定性。促成这样的设计是Javascript的事件循环和对回调的使用，它们使得程序员可以编写对网络或I/O事件进行响应的异步代码。

就如读者在本章中所看到的阻塞和非阻塞示例那样，使用事件循环是另一个编程方工。有些开发人员称其为编写将里面翻到外面的程序，实际上关键思想是，将代码围绕着事件来构架而不是按照期待中的输入入顺序来构架。由于事件循环以单一进程为基础，所以为了确保高性能需要遵循以下的一些规则。
* 函数必须快速返回
* 函数不得阻塞
* 长时间运行的操作必须移到另一个进程中

在这样的上下文中，有些程序不适合于事件循环。如果程序或函数需要长时间运行才能完成处理，那么事件循环就不是个好的选择。Node.js所不适合的地方包括处理大量数据或者长时间运行计算等。Node.js旨在网络中推送数据并瞬间完成！！
