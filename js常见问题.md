#### JavaScript的数据类型

+ **原始类型（简单数据类型）：**
  + Number：数值型，范围在±2 53次方
    + 整型值和浮点值，整数和小数，
    + 还可以是进制的数值，如：数字前面是0，则是八进制->010=8，前面是0x则是16进制->0xa=10
  + String：字符串型，带引号的字段
    + 可以通过.length获取字符串长度
    + 通过"+"拼接字符串：字符串和其他类型拼接就一定是字符型->'12'+12='1212'
  + boolean：布尔值，true、false，等价于1和0
  + undefined：未定义，声明变量后没有给值。与数字相加结果是NaN
  + null：空值，声明某个变量为空。与数字相加结果还是数字。
  + Symbol：用于唯一的标识符，使用Symbol( )创建。
  + biglnt：可以是任意长度的整数，数字末尾加n，或者使用 BigInt()构造函数。
+ **对象->object（复杂数据类型）：**
  + Date对象：Date 对象用于处理日期和时间
  + Function对象：函数
  + Array对象：数组
  + RegExp对象：RegExp 对象表示正则表达式

#### 判断变量的类型e

1. **最常见的判断方法：typeof（返回结果都为字符串形式）**

   使用typeof能判断出四种，分别是**number，string，boolean，object，undefined，function，symbo**l剩余的均被检测为object

2. **已知对象类型:  instanceof**

   ![image-20200829210632854](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200829210632854.png)

3. **对象原型链判断方法： prototype 通用但很繁琐:**->Object.prototype.toString.call()，Object原型上返回数据格式。

4. **根据对象的构造器constructor进行判断**：看不懂

5. **jQuery方法： jquery.type()**：在使用时,一定要引入jquery文件,不然会报错

6. **严格运算符:  ===**

#### 数据类型转换

+ **转换为字符串**

  + 变量.toString()
  + String(变量)
  + **利用"+"拼接字符串->隐式转换**

+ **转换为数值型**

  + parseInt(字符串)：将字符串**转换为整数**，字符串的第一个字符需要是数字
  + parseFloat(字符串)：将字符串**转换为浮点数**，字符串的第一个字符需要是数字
  + Number(变量)
  + **利用算数运算 - * / 如："120" - "110" = 10->隐式转换**

+ **转换为布尔值：使用Boolean（变量）**

  + " " 空字符串
  + undefined
  + false
  + NaN
  + null
  + 0

  **只有以上的值会转换成false，其他都会转换为true**

#### 原型和原型链

+ **原型：**

  + 任何对象都有一个原型对象，这个原型对象由对象的内置属性_proto_指向它的构造函数的prototype指向的对象，即任何对象都是由一个构造函数创建的，但是不是每一个对象都有prototype，只有方法才有prototype。

    ```js
    function star(uname, age) { 
      this.uname = uname;
      this.age = age;
    }
    Star.prototype.sing = function() {
    	console.log('我会唱歌');
    }
    var ldh = new star('刘德华', 18);
    var zxy = new star('张学友', 19);
    ldh.sing(); 
    ```

    **ldh可以调用sing是因为ldh对象实例中有proto属性指向prototype原型对象，两者是相等的，因此可以调用**

+ **原型链：**

![image-20200831143955133](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200831143955133.png)

+ **总结：**
  + 我们需要牢记两点：①`__proto__`和`constructor`属性是**对象**所独有的；② `prototype`属性是**函数**所独有的，因为函数也是一种对象，所以函数也拥有`__proto__`和`constructor`属性。
  + `__proto__`属性的**作用**就是当访问一个对象的属性时，如果该对象内部不存在这个属性，那么就会去它的`__proto__`属性所指向的那个对象（父对象）里找，一直找，直到`__proto__`属性的终点**null**，再往上找就相当于在null上取值，会报错。通过`__proto__`属性将对象连接起来的这条链路即**我们所谓的原型链**。
  + `prototype`属性的**作用**就是让该函数所实例化的对象们都可以找到公用的属性和方法，即`f1.__proto__ === Foo.prototype`。
  + `constructor`属性的含义就是**指向该对象的构造函数**，所有函数（此时看成对象了）最终的构造函数都指向**Function**。

#### 闭包及优缺点

+ **什么是闭包**

  + 闭包指有权访问另一个函数作用域中变量的**函数**

    ```js
    function fn() {
    	var num = 10;
    	function fun() {
    		console.log(num);
    	}
    	fun();
    }
    fn(); // 结果打印10
    ```

    此时，fun函数可以访问其作用域外部的变量，因此就产生了闭包，被访问的num变量所在的fn函数就是闭包。

    **也可以在外部调用闭包**

    ```js
    function fn() {
    	var num = 10;
    	function fun() {
    		console.log(num);
    	}
    	return fun;
    }
    var f = fn();
    f(); // 结果打印10
    
    高级写法：
    function fn() {
    	var num = 10;
    	return function() {
    		console.log(num);
    	}
    }
    var f = fn();
    f(); // 结果打印10
    ```

+ **闭包的优缺**

  + 闭包三要素：

    + 嵌套结构的函数
    + 内部函数访问了外部函数的变量
    + 在外部函数的外面，调用内部函数
    
    ```js
  /*闭包的常见写法*/
    function fun(){
    var name = "haha";
      function innerFun(){
        console.log(name);
        }
        return innerFun;
    }
    fun()();
    /*显然当执行fun()();语句的时候，控制台会打印"haha"出来*/
    ```
    
  + 优点：
  
    + 闭包的主要作用就是延伸了变量的作用范围
    + 可以重复使用变量，并且不会造成变量污染
    + 可以用来定义私有属性和私有方法。
  
  + 缺点：
  
    + 比普通函数更占用内存，会导致网页性能变差，在IE下容易造成内存泄露。
  
      **因为**闭包就是能够访问外部函数变量的一个函数，而函数是必须保存在内存中的对象，所以位于函数执行上下文中的所有变量也需要保存在内存中，这样就不会被回收，如果一旦循环引用或创建闭包，就会占据大量内存，可能会引起内存泄漏。闭包在**处理速度**和**内存消耗**方面对脚本性能具有负面影响。

#### call/apply/bind

+ **call：**

  + 用法：xxx.call(this指针, 参数, 参数...)
  + 作用：
    + 可以调用函数
    + 可以改变函数内的this指向
    + call的主要作用可以实现继承：xxx.call(this指针（指向自己就可以调用别的函数的参数）, 参数, 参数...)

+ **apply：**

  + 用法：xxx.apply(this指针, 数组)

  + 作用：

    + 可以调用函数，也可以改变函数内的this指向

    + 但是他的参数必须是数组（伪数组）

    + apply的主要应用hi利用apply借助于数学内置对象进行运算，例如求最大值：

      ```js
      var arr = [1, 66 ,7, 88, 0]
      
      var max = Math.max.apply(Math, arr)
      ```

+ **bind：**

  + 用法：xxx.bind(this指针, 参数, 参数...)

  + 作用：

    + 不会调用函数，但可改变函数内的this指向

    + 调用后返回的是原函数改变this指向后产生的新函数，因此可以这样调用函数

      ```js
      var x = xx.bind(this指向);
      x();
      ```

    + 不想立即调用函数，还想改变指向时就可以调用，例如改变定时器内部的this指向。

#### DOM事件流和事件委托

+ **什么是DOM：**文档对象模型，就是一个编程接口

+ **DOM事件流：**

  1. 事件捕获阶段：DOM从上到下执行

  2. 处于目标阶段

  3. 事件冒泡阶段：DOM从下到上执行

     + 阻止事件冒泡：event.stopPropagation()

       ```js
       document.querySelector('#btn').addEventListener('click', function (event) {
           console.log("btn was clicked");
           event.stopPropagation();
       });
       ```

+ **事件委托：**就是委托父级帮忙处理子级的事情，例如：

  ```js
  window.onload = function(){
      var oUl = document.getElementById("ul1");
     oUl.onclick = function(){
          alert(123);
      }
  }
  ```

#### Cookie/storage

+ **cookie:**

  + 使用：

    + 机制：**客户端发送一个请求到服务器** --》 **服务器发送一个HttpResponse响应到客户端，其中包含Set-Cookie的头部** --》 **客户端保存cookie，之后向服务器发送请求时，HttpRequest请求中会包含一个Cookie的头部** --》**服务器返回响应数据**

    + 属性项：

      | 属性项     | 属性项介绍                                                   |
      | :--------- | :----------------------------------------------------------- |
      | NAME=VALUE | 键值对，可以设置要保存的 Key/Value，注意这里的 NAME 不能和其他属性项的名字一样 |
      | Expires    | 过期时间，在设置的某个时间点后该 Cookie 就会失效             |
      | Domain     | 生成该 Cookie 的域名，如 domain="[www.baidu.com](http://www.baidu.com)" |
      | Path       | 该 Cookie 是在当前的哪个路径下生成的，如 path=/wp-admin/     |
      | Secure     | 如果设置了这个属性，那么只会在 SSH 连接时才会回传该 Cookie   |

  + 特性：

    1. 生命周期为设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭（这时候cookie保存到硬盘），默认为浏览器关闭就失效——**会话cookie**（一般不存储在硬盘而是保存在内存里）
    2. 存储的大小不能超过4k
    3. 以键值对的形式存储使用
    4. 一般由服务器生成，用于标识用户身份
    5. cookie的作用是与服务器进行交互，作为http规范的一部分存在为webstorage

  + 缺点：

    1. Cookie的大小是受限的
    2. Cookie会被附加在每个HTTP请求中，所以无形中增加了流量。
    3. cookie还需要指定作用域，不可以跨域调用
    4. 由于在HTTP请求中的Cookie是明文传递的，所以安全性成问题。（除非用HTTPS）

+ **storage：**

  + sessionStorage：
    + 特性：
      1. 生命周期为关闭浏览器窗口
      2. 在同一个窗口（页面）下数据可以共享
      3. 以键值对的形式存储使用
      4. 存储的大小一般为5M
      5. 数据保存在session对象中
    + 使用：
      + 存储数据：sessionStorage.setItem(key, value)
      + 获取数据：sessionStorage.getItem(key, value)
      + 删除数据：sessionStorage.removeItem(key)
      + 删除所有数据：sessionStorage.clear()
  + localStorage： 
    + 特性：
      1. 生命周期永久有效，除非手动删除否则关闭页面也会存在
      2. 可以多窗口（页面）共享（同一浏览器内）
      3. 以键值对的形式存储使用
      4. 存储的大小约为20M，一般为5M
      5. 数据保存在客户端本地的硬件设备
    + 使用：
      + 存储数据：localStorage.setItem(key, value)
      + 获取数据：localStorage.getItem(key, value)
      + 删除数据：localStorage.removeItem(key)
      + 删除所有数据：localStorage.clear()

+ **三者区别：**

  + ookie始终在同源的http请求中携带，即使不需要，cookie在浏览器和服务器中来回传递。而localStorage和sessionStora仅仅在本地存储，不会好服务器通信，也不会自动把数据发送给服务器。
  + 存储大小不同，cookie为4kb左右；localStorage， sessionStorage可以达到5M
  + 数据有效期不同，sessionStorage仅在同源窗口中有效，关闭窗口就消失了，cookie可以设置过期时间，localStorage长期有效
  + localStorage， sessionStorage有现成的API， cookie需要程序员手动封装

#### 数组和对象的常见方法

+ **数组：**

| length                  | 设置或返回 数组中元素的数目                                  |
| :---------------------- | :----------------------------------------------------------- |
| slice[start,end)        | 返回从原数组中指定开始下标到结束下标之间的项组成的新数组（不影响原数组） |
| .                       | 1个参数：n.即：n到末尾的所有                                 |
| .                       | 2个参数：[start,end]                                         |
| splice()：              |                                                              |
| .                       | 删除：2个参数，起始位置，删除的项数                          |
| .                       | 插入：3个参数，起始位置，删除的项数，插入的项                |
| .                       | 替换：任意参数，起始位置，删除的项数，插入任意数量的项       |
| pop()                   | 删除数组的最后一个元素，减少数组的长度，返回删除的值。（无参） |
| push()                  | 将参数加载到数组的最后，返回新数组的长度。 （参数不限）      |
| shift()                 | 删除数组的第一个元素,数组长度减1，返回删除的值。 （无参）    |
| unshift()               | 向数组的开头添加一个或更多元素，并返回新的长度。（参数不限） |
| sort()                  | 按指定的参数对数组进行排序 ，返回的值是经过排序之后的数组（无参/函数） |
| concat(3,4)             | 把两个数组拼接起来。 返回的值是一个副本 （参数不限）         |
| join()                  | 将数组的元素组起一个字符串，以separator为分隔符，省略的话则用默认用逗号为分隔符 |
| indexOf()               | 从数组开头向后查找，接受两个参数，要查找的项(可选)和查找起点位置的索引 |
| lastIndexOf()           | 从数组末尾开始向前查找，接受两个参数，要查找的项(可选)和查找起点位置的索引 |
| every()                 | 对数组中的每一项运行给定函数，如果该函数对每一项都返回true，则返回true。 |
| filter()                | 对数组中的每一项运行给定函数，返回该函数会返回true的项组成数组。 |
| forEach()               | 对数组的每一项运行给定函数，这个方法没有返回值。             |
| map()                   | 对数组的每一项运行给定函数，返回每次函数调用的结果组成的数组。 |
| some()                  | 对数组的每一项运行给定参数，如果该函数对任一项返回true，则返回true。以上方法都不会修改数组中的包含的值。 |
| reduce()和reduceRight() | 缩小数组的方法，这两个方法都会迭代数组的所有项，然后构建一个最终返回的值。 |

**对象：**

| keys()    | 返回一个包含所有给定对象**自身**可枚举属性名称的数组。     |
| --------- | ---------------------------------------------------------- |
| values()  | 返回给定对象自身可枚举值的数组。                           |
| entries() | 返回给定对象自身可枚举属性的 `[key, value]` 数组。         |
| is()      | 比较两个值是否相同。所有 NaN 值都相等（这与==和===不同）。 |
| assign()  | 通过复制一个或多个对象来创建一个新的对象。                 |

#### new内部做了什么

var a = new A();

假设我们要创建一个构造函数A()的实例a，则必须使用new操作符。会经历以下4个步骤：

+ 在内存中创建一个新的空对象（var o=new Object();）

+ 将空对象的原型赋值为构造函数A的原型（o.__proto__=A.prototype;）

+ 执行构造函数中的代码，为空对象添加属性（A.call(o);），也可以理解为将构造器函数内部this指向新建的空对象。

+ 返回添加属性后的对象。

#### 防抖/节流

+ **函数防抖**：将多次操作合并为一次操作进行。原理是维护一个计时器，规定在delay时间后触发函数，但是在delay时间内再次触发的话，就会取消之前的计时器而重新设置。这样一来，只有最后一次操作能被触发。
+ **函数节流**：使得一定时间内只触发一次函数。原理是通过判断是否有延迟调用函数未执行。
+ **区别**： 函数节流不管事件触发有多频繁，都会保证在规定时间内一定会执行一次真正的事件处理函数，而函数防抖只是在最后一次事件后才触发一次函数。 比如在页面的无限加载场景下，我们需要用户在滚动页面时，每隔一段时间发一次 Ajax 请求，而不是在用户停下滚动页面操作时才去请求数据。这样的场景，就适合用节流技术来实现。

#### requestAnimationFrame

+ **优势：**最大的优势是**由系统来决定回调函数的执行时机**，**它能保证回调函数在屏幕每一次的刷新间隔中只被执行一次**，这样就不会引起丢帧现象，也不会导致动画出现卡顿的问题。
+ **CPU节能：**使用setTimeout实现的动画，当页面被隐藏或最小化时，setTimeout 仍然在后台执行动画任务，由于此时页面处于不可见或不可用状态，刷新动画是没有意义的，完全是浪费CPU资源。而requestAnimationFrame则完全不同，当页面处理未激活的状态下，该页面的屏幕刷新任务也会被系统暂停，因此跟着系统步伐走的requestAnimationFrame也会停止渲染，当页面被激活时，动画就从上次停留的地方继续执行，有效节省了CPU开销。
   **函数节流：**在高频率事件(resize,scroll等)中，为了防止在一个刷新间隔内发生多次函数执行，使用requestAnimationFrame可保证每个刷新间隔内，函数只被执行一次，这样既能保证流畅性，也能更好的节省函数执行的开销。

#### this指向

+ 普通函数：this指向window
+ 构造函数：this指向实例对象，原型对象里面的方法也指向实例对象
+ 对象方法调用：this指向该方法所属对象
+ 事件绑定方法：this指向绑定事件对象
+ 定时器函数：this指向window
+ 立即执行函数：this指向window

#### 作用域链

​	一般情况下，变量取值到 创建 这个变量 的函数的作用域中取值。

　　但是如果在**当前作用域中没有查到值，就会向上级作用域去查，直到查到全局作用域，这么一个查找过程形成的链条就叫做作用域链。**

#### let/const/var的区别

+ **var：**修饰的变量，是函数级作用域（不支持块级作用域，在函数内支持），可以重复定义，会变量提示
+ **let：**修饰的变量，是块级作用域，不可以重复定义，不会变量提示
+ **const：**修饰的变量，是无法修改的，一半用于定义常量，不可以重复定义，不会变量提示。一旦声明必须赋值，声明后不能再修改，如果声明的是复合类型数据，可以修改其属性

#### ES6异步编程：promise和async await

+ **promise：**

  + 用法

    ```js
    let p = new Promise((resolve,reject) => {
        //...
        resolve('success')
    });
    
    p.then(res => {
        console.log(res);//success
    }).catch(err => {
      	console.log(err);
    });
    ```

  + 快捷写法：Promise.resolve()和Promise.reject()

  + **Promise.all()：**将多个Promise实例包装成一个新的Promise实例。

    **所有状态都是成功状态才返回数组，只要有reject就返回reject的状态值**

    ```js
    let p1 = Promise.resolve(123);
    let p2 = Promise.resolve('hello');
    let p3 = Promise.resolve('success');
    
    
    Promise.all([p1,p2,p3]).then(result => {
        console.log(result);
    })
    ```

  + **Promise.race()：**将多个Promise实例包装成一个新的Promise实例，**但不同的是里面的Promise实例是竞赛状态，那个实例返回的状态快，就返回这个状态。**

+ **async函数：**async函数用于声明一个函数是异步的，其**返回的是一个Promise对象**。

  + 基本语法

    ```js
    async function demo() {
    
    }
    demo();
    ```

+ **await：**awsit只能在async函数里面执行（放到普通函数里面会报错），await后面应该跟着promise对象，也可以是其他的返回值。

  ```js
  async function demo() {
      let result = await Promise.resolve(123);
      console.log(result);
  }
  demo();
  ```

#### 箭头函数

+ **使用**

  ```
  ()=> {}  
  ```

+ **其特性：**

  + 不能为箭头函数命名，因为箭头函数是一个函数表达式，是一个匿名函数
  + 当只有一个参数或只有一个表达式时，可以不添加()或{}
  + 如果返回一个对象时，需要()=> ({key:x})用小括号包括大括号
  + 箭头函数this为父作用域的this，不是普通函数调用时的this指向的对象
  + 箭头函数不能作为构造函数，不能使用new，不会自动生成prototype属性，也就是原型属性
  + 箭头函数没有arguments，super，new.target，但是可以调用外围的。如果箭头函数在一个function内部，它会将外部函数的arguments拿过来使用。箭头函数中要想接收不定参数，应该使用rest参数...解决。
  + 箭头函数通过bind、call和apply调用，不会改变this指向，只会传入参数
  
+ **和普通函数的区别：**

  ![image-20200831210735267](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200831210735267.png)

#### JavaScript的运行机制

​	**javascript 代码运行分两个阶段**：

​	1、预解析---把所有的函数定义提前，所有的变量声明提前，变量的赋值不提前

​	2、执行---从上到下执行（按照js运行机制）

​	由于JS是单线程运行，因此任务等待的时间可能会很长。因此JS将任务分为两种，**一种是同步任务（synchronous），另一种是异步任务（asynchronous）**。

+ **同步和异步：**

  + 同步任务：同步任务都在主线程上执行，形成一个执行栈。

  + 异步任务：JS的异步是通过回调函数实现的，一般而言，异步任务有一下三种类型：

    1. 普通事件，如click、resize等
    2. 资源加载，如load、error等
    3. 定时器，包括selInterval、setTimeout等
    4. DOM事件
    5. ES6中的Promise
    6. Ajax异步请求

    异步任务相关**回调函数添加到任务队列**中（任务队列也称为消息队列）

+ **运行机制：**

  1. 先执行执行栈中的同步任务
  2. 异步任务（回调函数）放入任务队列中
  3. 一旦执行占中的所有同步任务执行完毕，系统就会按次序读取任务队列中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈，开始执行。

+ **事件循环：**

  ![image-20200831180559665](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200831180559665.png)

#### 实现继承的几种方式

+ **原型链继承：**
+ **构造继承：**
+ **实例继承：**
+ **拷贝继承：**
+ **组合继承：**
+ **寄生组合继承：**

#### 垃圾回收

+ **目的：**JS垃圾回收机制的目的是为了防止内存泄漏，内存泄漏是指有一些已经不被需要的变量但仍然存在在内存中，这样便会造成内存泄漏。垃圾回收机制就是为了回收这些不被需要的变量，并且释放掉他们所指向的内存。
+ **方法：**
  + 标记清除：
    + 这是最常见的回收方法，也是大部分浏览器使用的回收方法。
    + 当变量进入执行环境是，就会被标记上“进入环境”，从逻辑上讲，被标记上“进入环境”的变量所指向的内存是永远不会被回收的。当某个变量离开执行环境时，就会被标上“离开环境”。被标记为“离开环境”的变量则是可以回收的。
  + 引用计数
    - 这是一种不太常见的回收方式。引用计数法就是同级引用类型声明后被引用的次数，当次数为0时，该变量就会被回收。

+ **有可能造成内存泄漏的案例**
  + 全局变量造成的内存泄漏
  + 未销毁的定时器和回调函数造成的内存泄漏
  + DOM引用造成的内存泄漏