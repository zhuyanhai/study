<p class="lead">
    <a href="http://study.utan.com/JS/学习路线">JS 学习路线</a> > JS 基础篇_this关键字
</p>

<pre><code class="nohighlight">
    this是JavaScript中的关键字之一，在编写程序的时候经常会用到，正确的理解和使用关键字this尤为重要

    **全局作用域中的this**
    <code language="javascript">
        console.log(this); //Window全局对象
        [desc]在全局作用域内，我们可以通过this访问到所有的全局属性，如下代码演示：[/desc]
        var a = 1;
        alert(this.a);
    </code><hr/>
    **函数作用域中的this**
    <code language="javascript">
        [desc]✪ 直接调用函数，this指向的是window对象[/desc]
        var a = 1;
        function test()
        {
            var a = 2;
            console.log(this.a); // 1
        }
        test();
        [desc]上述代码的打印结果仍是1，因为this指向的仍是window对象，那么怎样才能让this指向函数本身呢？继续观察[/desc]
        [desc]✪ 作为对象的方法调用[/desc]
        var a = 1;
        function test()
        {
            console.log(this.a); // 2
        }
        var obj = {a: 2, fn: test};
        obj.fn();
        [desc]上述代码的打印结果是2，因为this指向的是当前调用该方法的对象[/desc]
        [desc]✪ 作为构造函数调用[/desc]
        var a = 1;
        function test()
        {
            this.a = 2;
        }
        var obj = new test();
        console.log(obj.a); // 2
        [desc]上述代码的打印结果是2，因为this指向的是该构造函数创建的对象。[/desc]
        [desc]✪ 通过call或apply方法调用，call和apply都是Function对象的方法，都可以用来动态改变this的指向，达成函数复用的目的[/desc]
        var a = 1;
        function test()
        {
            console.log(this.a); // 1
        }
        test.call();
        [desc]call方法的第一个参数是this，在没有实参的情况下，this默认指向的对象就是window对象[/desc]
        var a = 1;
        function test()
        {
            console.log(this.a); // 1
        }
        var obj = {a: 2, fn: test};
        obj.fn.call();
        [desc]上面的例子进一步证明了，即便使用对象的方法调用call，this默认指向的依旧是全局对象。为了改变this的指向，我们需要显式的传递第一个参数过去，如下代码：[/desc]
        var a = 1;
        function test()
        {
            console.log(this.a); // 2
        }
        var obj = {a: 2};
        test.call(obj);
        [desc]✪ 嵌套函数作用域中的this[/desc]
        var a = 1;
        function test()
        {
            console.log(this.a); // 2
            function test2(){
                console.log(this.a); // 1
            }
            test2();
        }
        var obj = {a: 2, fn: test};
        obj.fn();
        [desc]上面的例子证明了正常调用内嵌函数，其中的this仍是window对象，如果想要this是其父函数的this，请参照以下代码：[/desc]
        var a = 1;
        function test()
        {
            console.log(this.a); // 2
            var self = this;
            function test2(){
                console.log(self.a); // 2
            }
            test2();
        }
        var obj = {a: 2, fn: test};
        obj.fn();
        [desc]上面的例子证明了存储一个父函数的this对象，在内嵌函数中就可以使用它（self）了。也可以通过call 或 apply调用，并指定第一个参数是其父函数对象[/desc]
    </code><hr/>
</code></pre>
        
<ul class="pager">
    <li style="float: left;"><a href="http://study.utan.com/JS/基础篇_作用域">◀基础篇_作用域</a></li>
    <li style="float: left;"><a href="http://study.utan.com/JS/基础篇_闭包">◀基础篇_闭包</a></li>
</ul>