#### 行内元素/块级元素，非替换元素/替换元素

+ **行内元素/块级元素**

  + 常见的元素

    + 块级（display：block）：div 、p、h1~h6、hr、ul、ol、li、dl、dd、form、table、header、footer、main、nav、sector、arcitcle、pre、table、tbody、thead、th、tr、tfoot
    + 行级（display：inline）：a、span、small、strong、em、i、code、
    + 行内块（display：inline-block）：img、input

  + 两者的区别

    1. 行内元素和其他行内元素都会在一条水平线上排列，都是在同一行的；块级元素却总是会在新的一行开始排列，各个块级元素独占一行，垂直向下排列，若想使其水平方向排序，可使用左右浮动（float：left/right）让其水平方向排列。

    2. 行内元素不可以设置宽高，宽度高度随文本内容的变化而变化，但是可以设置行高（line-height），同时在设置外边距margin上下无效，左右有效，内填充padding上下无效，左右有效；块级元素可以设置宽高，并且宽度高度以及外边距，内填充都可随意控制。

    3. 块级元素可以包含行内元素和块级元素，还可以容纳[内联元素](https://www.baidu.com/s?wd=内联元素&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)和其他元素；行内元素不能包含块级元素，只能容纳文本或者其他行内元素。

  + 三种元素之间的转换

    + 通过修改display属性:（display:block -> 转换为块级元素；display:inline -> 转换为行内元素；display:inline-block -> 转换为行内块级元素。）
    + 下面两个我不理解的方法

    > + float：当把行内元素设置完float:left/right后，该行内元素的display属性会被赋予block值，且拥有浮动特性。行内元素去除了之间的莫名空白。
    > + position：当为行内元素进行定位时，position:absolute，与position:fixed。都会使原先的行内元素变为块级元素。

+ **非替换元素/替换元素**

  + 替换元素就是浏览器根据元素的标签和属性，来决定元素的具体显示内容。替换元素是其内容不受CSS视觉格式化模型控制的元素，例如img标签，嵌入的文档（iframe之类）或者applet、input、textarea、select等这些叫做替换元素。
  + 非替换元素：(X)HTML 的大多数元素是非替换元素，他们将内容直接告诉浏览器，将其显示出来。
  + 行内替换元素，例如input,设置上下padding，可以撑大父元素。而行内非替换元素，如strong,设置上下padding，只是范围扩大，可是无法撑大父元素，不会影响line-height。

#### HTML5新增标签

以下答案只是新元素一部分

+ **布局标签**

  1. section：独立内容区块，可以用h1~h6组成大纲，表示文档结构，也可以有章节、页眉、页脚或页眉的其他部分；
  2. article：特殊独立区块，表示这篇页眉中的核心内容；
  3. aside：标签内容之外与标签内容相关的辅助信息；
  4. header：某个区块的头部信息/标题；
  5. footer：底部信息；
  6. nav：导航条部分信息；
  7. figure：独立的单元，例如某个有图片与内容的新闻块。
  8. hgroup：头部信息/标题的补充内容；

+ **表单标签**

  1. datalist：请与 input 元素配合使用该元素，来定义 input 可能的值。
  2. output：标签定义不同类型的输出，比如脚本的输出。

+ input输入类型

  **input:type=' email|url| number| range|week| datetime| datetime| search| tel|color'**

  （1）email：必须输入邮件；

  （2）url：必须输入url地址；

  （3）number：必须输入数值；

  （4）range：必须输入一定范围内的数值；

  （5）Date Pickers：日期选择器；

  a.date：选取日、月、年

  b.month：选取月、年

  c.week：选取周和年

  d.time：选取时间（小时和分钟）

  e.datetime：选取时间、日、月、年（UTC时间）

  f.datetime-local：选取时间、日、月、年（本地时间）

  （6）search：搜索常规的文本域；

  （7）color：颜色

+ **多媒体标签**

  1. video：视频
  2. audio：音频

+ **其他标签**

  1. mark：标注（像荧光笔做笔记）；
  2. progress：进度条；
  3. meter：定义度量衡，仅用于已知最大和最小值的度量；
  4. canvas：使用JS代码做内容进行图像绘制；

+ **新增的属性**

  + 全局属性
    1. hidden (隐藏元素)
  + input新属性
    1. required(必填)
    2. minlength(最小长度)
    3. maxlength(最大长度)
    4. pattern(正则表达式)
    5. placeholder(提示文本)
    6. autocomplete (自动填充)
    7. autofocus(自动获取焦点)

#### img标签的title和alt属性

+ **alt属性和title属性的相同点和区别**

  + 它们都会出现一个小浮层，显示图片相关的内容

  + 不同之处如下所示

    + alt属性的特点：

      1. 倘若图片加载不成功未能显示出来，就会在图片未显示的地方出现一段文字。这一作用是为了给未加载出来的图片提供信息，方便用户浏览网页，同时也方便开发人员维护网页。

      2. 搜索引擎可以通过这个属性的文字描述获取图片

    + title属性的特点：

      1. title属性可以用在任何元素上，当用户把鼠标移动到元素上时，就会出现title的内容，起到对图片说明的作用，其实质就是对图片的一种备注或者注释

    **通俗来讲，alt属性的实质是通过文字来代替图片的内容，而title属性的实质是对图片的描述或者注释。**

+ **显示情况：**

  + 仅设置title
    + 当图片正常显示时，当鼠标悬停图片时，可以看到图片的文字描述。
    + 当图片不正常显示时，未加载的地方会图片的文字描述
  + 仅设置alt属性时
    + 当图片正常显示时，用鼠标悬停图片之上，没有效果。
    + 当图片不正常显示时，未加载的地方会图片的文字描述
  + 同时设置了title属性和alt属性时，鼠标悬停时仅显示图片的title属性。

#### meta标签

+ **定义：**

  + meta标签提供关于 HTML 文档的元数据。它不会显示在页面上，但是对于机器是可读的。常用于定义页面的说明，关键字，最后修改日期，和其它的元数据。这些元数据将服务于浏览器（如何布局或重载页面），搜索引擎和其它网络服务。

+ **常用：**

  ![image-20200827214454810](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200827214454810.png)

#### DOCTYPE标签

+ **定义：**Doctype是document type(文档类型)的简写,用来告诉浏览器的解析器使用哪种HTML或XHTML规范解析页面。DOCTYPE不存在或格式不正确会导致文档以兼容模式呈现。文档类型有3种：Strict（严格）、Transitional（过渡）以及Frameset（基于框架）。

+ **标准模式和兼容模式：**标准模式的排版和JS运作模式都是以该浏览器支持的最高标准运行。在兼容模式中，页面以宽松的向后兼容的方式显示，模拟老式浏览器的行为以防止站点无法工作。简单的说，就是尽可能的能显示东西给用户看。

  具体的说二者的不同在于：

  + width不同

    + 在严格模式中 ：width是内容宽度 ，元素真正的宽度 = margin-left + border-left-width + padding-left + width + padding-right + border-right- width + margin-right;

    + 在兼容模式中 ：width则是元素的实际宽度 ，内容宽度 = width - ( padding-left + padding-right + border-left-width + border-right-width)

  + 设置百分比的高度和行内元素的高宽

    + 兼容模式下可设置百分比的高度和行内元素的高宽。

    + 在标准模式下，给span等行内元素设置wdith和height都不会生效，而在兼容模式下，则会生效。

    + 在标准模式下，一个元素的高度是由其包含的内容来决定的，如果父元素没有设置高度，子元素设置一个百分比的高度是无效的。

  + 用margin:0 auto设置水平居中在IE下会失效
    + 使用margin:0 auto在standards模式下可以使元素水平居中，但在兼容模式下却会失效（可用text-align属性解决）

  + 兼容模式下Table中的字体属性不能继承上层的设置，white-space:pre会失效，设置图片的padding会失效

+ **HTML5 为什么只需要!DOCTYPE HTML呢？**

  + DTD的是W3C所发布的一个文档类型定义，简单的说，就是告诉浏览器你的这个HTML，是根据那个标准写的，解析的时候用哪个标准解析。

    HTML5 不基于 SGML（标准通用标记语言），因此不需要对DTD进行引用，但是需要doctype来规范浏览器的行为（让浏览器按照它们应该的方式来运行）。

    而HTML4.01基于SGML,所以需要对DTD进行引用，才能告知浏览器文档所使用的文档类

#### script标签的defer和async

+ **没有这两个属性：**脚本的下载和执行将会按照文档的先后顺序同步进行。当脚本下载和执行的时候，文档解析就会被阻塞

  ![image-20200827221907098](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200827221907098.png)

+ **defer属性：**

  ![image-20200827222550020](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200827222550020.png)

+ **async属性：**

  ![image-20200827222246106](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200827222246106.png)

+ **两者区别：**

  + 当script中有defer属性时，脚本的加载过程和文档加载是异步发生的，等到文档解析完(DOMContentLoaded事件发生)脚本才开始执行。
  + 当script有async属性时，脚本的加载过程和文档加载也是异步发生的。但脚本下载完成后会停止HTML解析，执行脚本，脚本解析完继续HTML解析。
  + 当script同时有async和defer属性时，执行效果和async一致。

#### 有哪些盒子模型：重点->W3C盒模型和怪异盒模型（标准盒模型和IE盒模型）

+ **标准盒模型：**

  ![image-20200827233844925](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200827233844925.png)

  > **在标准的盒子模型中，width指content部分的宽度**

+ **ie/怪异盒模型：**

  ![image-20200827233925882](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200827233925882.png)

  >**在IE盒子模型中，width表示content+padding+border这三个部分的宽度**

+ **flex弹性伸缩盒模型**

+ **column多列布局**

#### 水平垂直居中的方法

```css
body{
  height: 100%;
  overflow: hidden;
}
.box {
  width: 100px;
  height: 50px;
  background: red;
}
```

+ 定位：3种

  + 盒子需要设定宽高，且需要计算盒子宽高

    ```css 
    body{
      height: 100%;
      overflow: hidden;
      position: relative;
    }
    .box {
      width: 100px;
      height: 50px;
      background: red;
      position: absolute;
      top:50%;
      left:50%;
      /* 到这一步就是设置了盒子的左上角位于屏幕的中心点*/
      margin-top:-25px;
      margin-left:-50px;
    }
    ```

  + 盒子需要设定宽高，不需要计算盒子宽高

    ```css
    body{
      height: 100%;
      overflow: hidden;
      position: relative;
    }
    .box {
      width: 100px;
      height: 50px;
      background: red;
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      margin: auto;
    }
    ```

  + 盒子不需要设置宽高，且不需要计算宽高，**但不兼容**

    ```css
    body{
      height: 100%;
      overflow: hidden;
      position: relative;
    }
    .box {
      background: red;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
    ```

+ display: flex->父元素需要固定高度，简单，但不兼容

  ```css
  body{
    height: 1000px;
    overflow: hidden;
    display:flex;
    justify-content: center;
    align-items: center;
  }
  .box {
    background: red;
  }
  ```

+ JavaScript->子元素的宽度需要设置

  ```css
  body{
  	position: relative;
    height: 1000px;
    overflow: hidden;
  }
  .box {
    background: red;
    width: 100px;
    height: 50px;
  }
  ```

  ```js
  let HTML = document.documentElement,
  	    winW = HTML.clientWidth,
  	    winH = HTML.clientHeight,
  	    boxW = box.offsetWidth,
  	    boxH = box.offsetHeight;
  		box.style.position = "absolute";
  		box.style.left = (winW - boxW) / 2 + 'px';
  		box.style.top = (winH - boxH) / 2 + 'px';
  ```

+ display: table-cell->父级元素需要固定宽高

  ```css
  body{
  		  height: 100px;
  		  overflow: hidden;
  		  display: table-cell;
  		  vertical-align: middle;
  		  text-align: center;
  		  width: 100px;
  		  border:1px solid #000;
  		}
  		.box {
  		  background: red;
  		  display: inline-block;
  		}
  ```

+ line-height->父级元素固定宽高

  ```css
  body{
  		  height: 300px;
  		  width: 300px;
  		  line-height: 300px;
      	text-align: center;
  		  border:1px solid #000;
  		}
  		.box {
  		  	font-size: 16px;
  		    display: inline-block;
  		    vertical-align: middle;
  		    line-height: initial;
  		    text-align: left; /* 修正文字 */
  		}
  ```

#### BFC

+ **BFC是什么？**

  W3C官方解释：它决定了元素如何对其内容进行定位以及与其他元素的关系和相互作用当涉及到可视化布局的时候 BloclFormatting Context提供了一个环境HTML元素在这个环境中按照一定规则进行布局。

  其实其目的就是：形成一个完全独立的空间，让空间中的子元素不会影响到外面的布局

+ **BFC的触发条件？**

  1. float不为none
  2. position不为relative和static
  3. overflow不为visible
  4. display的值为table-cell或inline-block、flex、table-caption或者inline-flex

+ **BFC的特性？**

  1. 内部的Box会在垂直方向，一个接一个地放置。

  2. Box垂直方向的距离由margin决定。属于**同一个**BFC的两个相邻Box的margin会发生重叠。

  3. 每个盒子（块盒与行盒）的margin box的左边，与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。

  4. BFC的区域不会与float box重叠。

  5. BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。

  6. 计算BFC的高度时，浮动元素也参与计算。

+ **BFC的作用？**

  + 解决浮动元素令父元素高度塌陷的问题（依据特性6）
  + 解决自适应布局的问题（依据特性3和4）
  + 解决外边距垂直方向重合问题（依据特性2）

  > 这些问题除了BFC布局的其他解决方法：
  >
  > https://www.bilibili.com/video/BV16b411H7Pz?from=search&seid=8010717593650943783

#### 清除浮动的方法

+ **额外标签法**（在最后一个浮动标签后，新加一个块级标签，给其设置clear：both；）（不推荐）
  + 优点：通俗易懂，方便
  + 缺点：添加无意义标签，语义化差
+ **BFC方法**（父级元素设置overflow:hidden；overflow:auto；）
  + 优点：简单，代码少，浏览器支持好
  + 缺点：内部宽高超过父级div时，会被隐藏或者出现滚动条。
+ **给父级元素设置高度**
  + 优点：简单，代码少，容易掌握
  + 缺点：不灵活
+ **父级元素一起浮动**
  + 优点：代码少
  + 缺点：会产生新的浮动问题。
+ **伪元素**
  + 优点：符合闭合浮动思想，结构语义化正确
  + 缺点：ie6-7不支持伪元素：after，使用zoom:1触发hasLayout.

#### position属性

​	position共5个属性：static（没有定位）->默认值、absolute（绝对定位）、relative（相对定位）、fixed（固定定位）、sticky（粘性定位）

+ **static**

  指定元素使用正常的布局行为，即元素在文档常规流中当前的布局位置。此时 top、right、bottom、left 属性无效。

+ **absolute**

  **指定元素相对于最近的非 static 定位祖先元素的偏移**，来确定元素位置。绝对定位的元素可以设置外边距（margin），且不会与其他边距合并。**会随着页面滚动变动位置**。脱离文档流，因此不占据空间，所以**会和其他元素发生重叠**。

+ **relative**

  **相对于自己本应该在的位置，通过top、bottom、left、right定位**。不会脱离文档流。position:relative 对 table-*-group, table-row, table-column, table-cell, table-caption 元素无效。

+ **fixed**

  fixed定位是指元素的位置**相对于浏览器窗口是固定位置**，即使窗口是滚动的他也不会滚动，而且fixed定位使元素的位置与文档流无关，因此不占据空间，所以会和其他元素发生重叠。没设置top、bottom、left、right时，可以存在在父级元素里面，设置后只会根据窗口定位。

+ **sticky**

  设置top、bottom、left、right后，元素呆在原本位置，当元素到达设定位置时，即元素原本位置滚动超过设置位置时，就会固定在设定位置。若滚动没有超出设定位置，则随页面滚动。（个人理解）例子：滚动导航栏，到达顶部固定在顶部。

#### CSS隐藏元素的方式

+ **opacity:0**

  **浏览器不会进行重排不会进行重绘，只是降低了alpha的数值达到透明**

  opacity属性的意思是设置一个元素的透明度。这一位着将opacity设置为0只能从视觉上隐藏元素。而元素本身依然占据它自己的位置并对网页的布局起作用，它也将响应用户交互。

+ **visibility:hidden**

  **浏览器不会进行重排但是会进行了重绘，重新绘制元素信息；transition有效果**

  第二个要说的属性是visibility。将它的值设为hidden将隐藏我们的元素。如同opacity属性，被隐藏的元素依然会对我们的网页布局起作用。与opacity唯一不同的是它不会响应任何用户交互。此外元素在读屏软件中会被隐藏

    注意，如果一个元素的visibility被设置为hidden，同时想要显示它的某个子孙元素，只要将那个元素的visibility显式设置为visible即可。

+ **diaplay:none**

  **display属性在none和其他属性切换时：浏览器进行了重排和重绘的操作，重新安排页面元素位置以及重新绘制元素信息；transition没效果**

   display属性依照词义真正隐藏元素。将display属性设为none确保元素不可见并且连盒模型也不生成。使用这个属性，被隐藏的元素不占据任何空间。不仅如此，一旦display设为none任何对该元素直接打用户交互操作都不可能生效。此外，读屏软件也不会读到元素的内容。这种方式产生的效果就像元素完全不存在。

    任何这个元素的子孙元素也会被同时隐藏。为这个属性添加过度动画是无效的，他的任何不同状态值之间的切换总是会立即生效。

    不过请注意，通过DOM依然可以访问到这个元素。因此你可以通过DOM来操作它。

**以上三者的差别：**

![image-20200828171707568](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200828171707568.png)

+ **position:absolute**

  假设有一个元素你想要与它交互，但是你又不想让它影响你的网页布局，没有合适的属性可以处理这种情况（opacity和visibility影响布局mdisplay不影响布局但又无法直接交互）。在这种情况下，只能考虑将元素移出可视区域。这个办法既不会影响布局，有可能让元素保持可以操作。

  .hide {
    position: absolute;
    top: -9999px;
    left: -9999px;

  }

+ **clip-path**

   隐藏元素的另一种方法是通过剪裁它们实现。

  .hide {
   clip-path: polygon(0px 0px,0px 0px,0px 0px,0px 0px);

  }

#### Flex布局

#### 双栏布局 三栏布局

#### 重排和重绘

#### CSS选择器

#### CSS动画

#### CSS实现三角形

#### CSS Sprites

#### px rem em 

1. px像素（Pixel）。相对长度单位。像素px是相对于显示器屏幕分辨率而言的。浏览器默认字体大小为16px。

2. em是相对长度单位，相对于当前对象内文本的字体大小，但当当前对象没有设置字体大小时，**em会继承父级元素的字体大小**。例如：

   ```css
   .div1 {
   	background: Lightblue;
   	font-size: 20px;
   	height: 10em;
   	width: 10em;
   }
   .div2 {
     background: Lightpink;
     font-size: 10px;
     height: 10em;
     width: 10em;
     /* 10em = 100px */
     /* 10 x 10 = 100 */
   }
   .div3 {
     background: Lightgreen;
     height: 100px;
     width: 100px;
   }
   ```

   效果图：

   **（div1是div2和div3的父级，因此1em = 20px，若父级组件没有设置则继承根元素。）**

   ![image-20200827180009008](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200827180009008.png)

3. rem是[CSS3](http://www.html5cn.org/portal.php?mod=list&catid=16)新增的一个相对单位（root em，根em），仍然是相对大小，**但相对的只是HTML根元素（即root选择器和html选择器下设置的字体大小，:root{}==html{}）**。

   ```css
   html {
   	color: red;
   	font-size: 2rem;
   	/* 2 x 16px = 32px */
   }
   .divi {
   	font-size: 2rem;
   	/* 2 x 32px = 64px */
   }
   .div2 {
   	font-size: 64px;
   }
   .div3 { 
   	font-size: 3rem;
   	/* 3x 32px = 96px */
   }
   .div4 {
   	font-size: 96px;
   }
   ```

   

##### 伪类/伪元素