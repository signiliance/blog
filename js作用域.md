###  1 -  js 作用域

####     静态作用域

作用域是指程序源代码中定义变量的区域。

作用域规定了如何查找变量，也就是确定当前执行代码对变量的访问权限。

大多数现在程序设计语言都是采用静态作用域规则，如[C/C++](https://zh.wikipedia.org/wiki/C/C%2B%2B "C/C++")、[C#](https://zh.wikipedia.org/wiki/C%E2%99%AF "C♯")、[Python](https://zh.wikipedia.org/wiki/Python)、[Java](https://zh.wikipedia.org/wiki/Java "Java")、[JavaScript](https://zh.wikipedia.org/wiki/JavaScript "JavaScript")……

JavaScript 采用词法作用域(lexical scoping)，也就是静态作用域。

因为 JavaScript 采用的是词法作用域，函数的作用域在函数定义的时候就决定了。

而与词法作用域相对的是动态作用域，函数的作用域是在函数调用的时候才决定的。

让我们认真看个例子就能明白之间的区别：

``` var value = 1;

function foo() {
    console.log(value);
}

function bar() {
    var value = 2;
    foo();
}

bar();

//  1
```
假设JavaScript采用静态作用域，让我们分析以下执行过程：

执行 foo() ，先从 foo 函数内部查询是否有局部变量 value ，如果没有，就根据书写的位置，查找上面一层的代码，也就是 value = 1，所以结果会打印 1。

假设JavaScript采用动态作用域，让我们分析以下执行过程：

执行 foo() ，依然是从 foo 函数内部查找是否有局部变量 value ，如果没有，就从调用函数的作用域，也就是 bar 函数内部查找是否有 value 变量，所以结果会打印 2 。

前面已经说了， JavaScript 采用的是静态作用域， 所以这个例子的结果是1。

但是，使用 eval()  和  with，this 可以产生动态作用域的效果。

####     动态作用域

既然js是静态作用域，那么什么是动态作用域呢？

采用动态作用域的语言有[Pascal](https://zh.wikipedia.org/wiki/Pascal "Pascal")、[Emacs Lisp](https://zh.wikipedia.org/wiki/Emacs_Lisp "Emacs Lisp")、[Common Lisp](https://zh.wikipedia.org/wiki/Common_Lisp "Common Lisp")（兼有静态作用域）、[Perl](https://zh.wikipedia.org/wiki/Perl "Perl")（兼有静态作用域）。C/C++是静态作用域语言，但在宏中用到的名字，也是动态作用域。

举个栗子：

bash（unix shell的一种） 就是动态作用域。以下脚本：

```  value=1
function foo () {
    echo $value;
}
function bar () {
    local value=2;
    foo;
}
bar
```
如果你不信的话，可以把以上代码，存为 scope.bash。然后进入相应目录下 执行 bash scope.bash，看看打印的结果是多少～

#### 想想

让我看一个 《JavaScript 权威指南》中的例子：

``` var scope = "global scope";
function checkscope(){
    var scope = "local scope";
    function f(){
        return scope;
    }
    return f();
}
checkscope();
```
``` var scope = "global scope";
function checkscope(){
    var scope = "local scope";
    function f(){
        return scope;
    }
    return f;
}
checkscope()();
```
以上两段代码的执行结果都是： local scope。

那么原因是什么呢：javascipt采用词法作用域，函数的作用域基于函数创建的位置。

引用《JavaScript 权威指南》的回答就是：

JavaScript 函数的执行用到了作用域链，这个作用域链是在函数定义的时候创建的。嵌套的函数 f() 定义在这个作用域链里，其中的变量 scope 一定是局部变量，不管何时何地执行函数 f()，这种绑定在执行 f() 时依然有效。

但是有一个值得思考的问题就是：

虽然两段代码执行的结果一样，但是两段代码究竟有什么不同呢？

那么就要牵扯到更多内容了，词法作用域只是其中一小部分。执行上下文栈也是其中一部分，让我们期待下一篇文章。