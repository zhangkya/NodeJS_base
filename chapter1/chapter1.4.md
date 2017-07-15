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
      $(function(){
        $('p').hide{'slow'};
        alert("The paragraph is now hidden");
        })
    </script>
  </body>
</html>
```
