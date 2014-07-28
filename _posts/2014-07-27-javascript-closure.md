---
                  layout: post
                  title: "Javascript closure"
                  description: ""
                  category: 
                  tags: [javascript]
---
{% include JB/setup %}
#Javascript中的闭包
好吧，今天尝试整理一下闭包相关的概念。
##闭包是什么。
看这段代码：
{% highlight javascript %}
var foo = ( function() {
    var privateThing = 'joe';
    // “闭包”内的函数可以访问 privateThing，而 privateThing 对于外部却是隐藏的
    return {
        get_thing: function () {
            // 通过接口来访问 privateThing
            return privateThing;
        },
        set_thing: function ( new_value ) {
            // 通过接口来修改 privateThing
            privateThing = new_value;
        }
    };
} () );

foo.get_thing (); // 得到 privateThing
foo.privateThing; // 访问不到，出错
foo.set_thing ('a new thing'); // 通过函数接口，我们访问并修改了 privatThing 变量
foo.get_secret (); // 得到 'a new thing'
{% endhighlight %}
这里，`foo`中包含两个闭包：函数`get_thing`, 函数`set_thing`;这两个函数都维持着对外部作用域function的引用，因此总可以访问作用域中的变量`privateThing`。
因为javascript中不可以对作用域进行引用或者赋值，因此没有办法在外部访问变量`privateThing`。唯一的途径是通过那两个闭包。
然后我们就不难理解闭包的概念了：**闭包是指，内部函数总是可以访问其所在外部函数中声明的参数和变量，即使在其外部函数被返回了之后。**(Douglas Crockford)
##闭包的应用场景。
Javascript中，利用闭包可以实现私有变量，私有方法。如前例所示。
##Javascript中闭包相关的实现。
Javascript满足了实现闭包的一些条件：

 - first-class function；
 - 可以嵌套定义函数；
 - 可以捕获引用环境，并把引用环境和函数代码组成一个可调用的实体；
 - 允许定义匿名函数；

第一点first-class function指的是，javascript中，函数可以作为参数传递，也可以作为return value, 可以复制给变量，就像字符串，整数等简单类型一样。
第三点基本是通过词法作用域lexical scope实现的。
词法作用域是指，一个变量的作用域是取决于这个变量定义在源代码中的位置，对于嵌套定义的函数，内部函数能获取到外部作用域中的变量。

明确了`first-class function`和 `lexical scope`的概念以后，在回头看第一个例子：
变量`foo`被赋值为一个对象，这个对象包含两个成员方法`get_thing`和`set_thing`,这在js中是合法的因为函数是可以作为返回值的。当调用`foo.get_thing()`时，引用到了变量`privateThing`，根据词法作用域，`foo.get_thing()`可以获取到变量`privateThing`，虽然此时外部的函数已经执行完毕了。
所以说，在没有闭包的语言中，变量的生命周期只限于创建它的环境。但在有闭包的语言中，只要有一个闭包引用了这个变量，它就会一直存在。清理不被任何函数引用的变量的工作通常由垃圾回收完成。










