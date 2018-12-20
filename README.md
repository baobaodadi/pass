# 总结
## ES5
## JS APIs和JS语法的区别

```
api是什么？Application Programming Interface， 应用程序编程接口。就是说它能给你提供一些方法，使你的开发变得简洁。它并不是什么技术，说白了就是一种语言提供的默认的方法的集合。不如js数组的push方法，当你想往数组里添加元素的时候，不用循环来实现了，直接push就能把元素加进去了，这个push方法就是js提供给你的一个api。
```
##### javascript有哪几种数据类型
```
六种基本数据类型
* undefined
* null
* string
* boolean
* number
* symbol(ES6)
一种引用类型
* Object
```
## ES6
在使用新的ES6技巧时千万不要做过了头，使你的代码比你或者你的其他队友聪明
##### 什么是Babel，什么是Shims/Polyfills

Babel 是一个通用的多用途 JavaScript 编译器。通过 Babel 你可以使用（并创建）下一代的 JavaScript，以及下一代的 JavaScript 工具。

Babel 把用最新标准编写的 JavaScript 代码向下编译成可以在今天随处可用的版本。 这一过程叫做“源码到源码”编译， 也被称为转换编译（transpiling，是一个自造合成词，即转换＋编译。以下也简称为转译）。
https://github.com/jamiebuilds/babel-handbook/blob/master/translations/zh-Hans/user-handbook.md

Polyfill（代码填充，也可译作兼容性补丁） 的技术。 简单地说，polyfill 即是在当前运行环境中用来复制（意指模拟性的复制，而不是拷贝）尚不存在的原生 api 的代码。 能让你提前使用还不可用的 APIs
##### 什么是块作用域:{}

```
let
	{
	console.log( a );	// undefined
	console.log( b );	// ReferenceError!

	var a;
	let b;
}
const
{
	const a = [1,2,3];
	a.push( 4 );
	console.log( a );		// [1,2,3,4]

	a = 42;					// TypeError!
}
```
##### 词法作用域和动态作用域，this和=>

```
动态作用域不关心它本身是怎样在哪里声明的，只关心它在哪里调用的，动态作用域的域链基于调用栈，而不是代码中的嵌套关系。
词法作用域关心的是函数在哪里声明的，动态作用域的概念和js中的this相同，this也关心函数在哪里调用的。
```
## REACT

```
React面试题
1.react解决什么问题
用于构建 UI 的
React 是 Reactive Programming 在 Web User Interface 上实现的手段，它只不过是一个库，提供了reactive render, component system 和降低开销的 DOM diff 算法. 把 React 换掉，只要不是手动操作 DOM, 其它的框架也不过大同小异。

1、redux中间件
中间件提供第三方插件的模式，自定义拦截 action -> reducer 的过程。变为 action -> middlewares -> reducer 。这种机制可以让我们改变数据流，实现如异步 action ，action 过滤，日志输出，异常报告等功能。
常见的中间件：
redux-logger：提供日志输出
redux-thunk：处理异步操作
redux-promise：处理异步操作，actionCreator的返回值是promise
 
2、redux有什么缺点
1.一个组件所需要的数据，必须由父组件传过来，而不能像flux中直接从store取。
2.当一个组件相关数据更新时，即使父组件不需要用到这个组件，父组件还是会重新render，可能会有效率影响，或者需要写复杂的shouldComponentUpdate进行判断。
 
3、react组件的划分业务组件技术组件？
根据组件的职责通常把组件分为UI组件和容器组件。
UI 组件负责 UI 的呈现，容器组件负责管理数据和逻辑。
两者通过React-Redux 提供connect方法联系起来。
具体使用可以参照如下链接：http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_three_react-redux.html
 
4、react生命周期函数
这个问题要考察的是组件的生命周期
一、初始化阶段：
getDefaultProps:获取实例的默认属性
getInitialState:获取每个实例的初始化状态
componentWillMount：组件即将被装载、渲染到页面上
render:组件在这里生成虚拟的DOM节点
componentDidMount:组件真正在被装载之后
二、运行中状态：
componentWillReceiveProps:组件将要接收到属性的时候调用
shouldComponentUpdate:组件接受到新属性或者新状态的时候（可以返回false，接收数据后不更新，阻止render调用，后面的函数不会被继续执行了）
componentWillUpdate:组件即将更新不能修改属性和状态
render:组件重新描绘
componentDidUpdate:组件已经更新
三、销毁阶段：
componentWillUnmount:组件即将销毁
 
5、react性能优化是哪个周期函数？
shouldComponentUpdate 这个方法用来判断是否需要调用render方法重新描绘dom。因为dom的描绘非常消耗性能，如果我们能在shouldComponentUpdate方法中能够写出更优化的dom diff算法，可以极大的提高性能。
详细参考：
https//segmentfault.com/a/1190000006254212 
 
6、为什么虚拟dom会提高性能?
虚拟dom相当于在js和真实dom中间加了一个缓存，利用dom diff算法避免了没有必要的dom操作，从而提高性能。
具体实现步骤如下：
用 JavaScript 对象结构表示 DOM 树的结构；然后用这个树构建一个真正的 DOM 树，插到文档当中
当状态变更的时候，重新构造一棵新的对象树。然后用新的树和旧的树进行比较，记录两棵树差异
把2所记录的差异应用到步骤1所构建的真正的DOM树上，视图就更新了。
参考链接：
https://www.zhihu.com/question/29504639?sort=created
 
7、diff算法?
把树形结构按照层级分解，只比较同级元素。
给列表结构的每个单元添加唯一的key属性，方便比较。
React 只会匹配相同 class 的 component（这里面的class指的是组件的名字）
合并操作，调用 component 的 setState 方法的时候, React 将其标记为 dirty.到每一个事件循环结束, React 检查所有标记 dirty 的 component 重新绘制.
选择性子树渲染。开发人员可以重写shouldComponentUpdate提高diff的性能。
参考链接：
https//segmentfault.com/a/1190000000606216 
8、react性能优化方案
（1）重写shouldComponentUpdate来避免不必要的dom操作。
（2）使用 production 版本的react.js。
（3）使用key来帮助React识别列表中所有子组件的最小变化。
参考链接：
https://segmentfault.com/a/1190000006254212

 
9、简述flux 思想
Flux 的最大特点，就是数据的"单向流动"。
1.用户访问 View
2.View 发出用户的 Action
3.Dispatcher 收到 Action，要求 Store 进行相应的更新
4.Store 更新后，发出一个"change"事件
5.View 收到"change"事件后，更新页面

```
## CSS

```
CSS面试题

 1.介绍一下标准的CSS的盒子模型？与低版本IE的盒子模型有什么不同的？
标准盒子模型：宽度=内容的宽度（content）+ border + padding + margin低版本IE盒子模型：宽度=内容宽度（content+border+padding）+ margin
2 box-sizing属性？
用来控制元素的盒子模型的解析模式，默认为content-boxcontext-box：W3C的标准盒子模型，设置元素的 height/width 属性指的是content部分的高/宽border-box：IE传统盒子模型。设置元素的height/width属性指的是border + padding + content部分的高/宽
3 CSS选择器有哪些？哪些属性可以继承？
CSS选择符：id选择器(#myid)、类选择器(.myclassname)、标签选择器(div, h1, p)、相邻选择器(h1 + p)、子选择器（ul > li）、后代选择器（li a）、通配符选择器（*）、属性选择器（a[rel=”external”]）、伪类选择器（a:hover, li:nth-child）
可继承的属性：font-size, font-family, color
不可继承的样式：border, padding, margin, width, height
优先级（就近原则）：!important > [ id > class > tag ]!important 比内联优先级高

Given the HTML below:
1. <ul class="shopping-list" id="awesome">
2.     <li><span>Milk</span></li>
3.     <li class="favorite" id="must-buy"><span class="highlight">Sausage</span></li>
4. </ul>
What is the color of the text Sausage ?
ul#awesome {
    color: red;
}
ul.shopping-list li.favorite span {
    color: blue;
}

4 CSS优先级算法如何计算？
元素选择符： 1 class选择符： 10. id选择符：100.  元素标签：1000
1. !important声明的样式优先级最高，如果冲突再进行计算。 
2. 如果优先级相同，则选择最后出现的样式。 
3. 继承得到的样式的优先级最低
4.  
较同一级别的个数，数量多的优先级高，如果相同即比较下一级别的个数 ，至于各级别的优先级，大家应该已经很清楚了，就是：
important > 内联 > ID > 类 > 标签 | 伪类 | 属性选择 > 伪对象 > 继承 > 通配符 通配符 > 继承

5 CSS3新增伪类有那些?
p:first-of-type 选择属于其父元素的首个元素p:last-of-type 选择属于其父元素的最后元素p:only-of-type 选择属于其父元素唯一的元素p:only-child 选择属于其父元素的唯一子元素p:nth-child(2) 选择属于其父元素的第二个子元素:enabled :disabled 表单控件的禁用状态。:checked 单选框或复选框被选中。
6 如何居中div？如何居中一个浮动元素？如何让绝对定位的div居中？
div：
border : 1px solid red;
margin : 0 auto ;
height : 50px ;
width : 80px ;
浮动元素的上下左右居中：
border : 1px solid red;
float : left ;
position : absolute ;
width : 200px ;
height : 100px ;
left : 50 %;
top : 50 %;
margin : -50px 0 0 -100px ;
绝对定位的左右居中：
border : 1px solid black;
position : absolute ;
width : 200px ;
height : 100px ;
margin : 0 auto ;
left : 0 ;
right : 0 ;

还有更加优雅的居中方式就是用flexbox，我以后会做整理。
7 display有哪些值？说明他们的作用?
inline（默认）–内联none–隐藏block–块显示table–表格显示list-item–项目列表inline-block
8 position的值？
static（默认）：按照正常文档流进行排列；relative（相对定位）：不脱离文档流，参考自身静态位置通过 top, bottom, left, right 定位；absolute(绝对定位)：参考距其最近一个不为static的父级元素通过top, bottom, left, right 定位；fixed(固定定位)：所固定的参照对像是可视窗口。
9 CSS3有哪些新特性？
1. RGBA和透明度 
2. background-image background-origin(content-box/padding-box/border-box) background-size background-repeat 
3. word-wrap（对长的不可分割单词换行）word-wrap：break-word 
4. 文字阴影：text-shadow： 5px 5px 5px #FF0000;（水平阴影，垂直阴影，模糊距离，阴影颜色） 
5. font-face属性：定义自己的字体 
6. 圆角（边框半径）：border-radius 属性用于创建圆角 
7. 边框图片：border-image: url(border.png) 30 30 round 
8. 盒阴影：box-shadow: 10px 10px 5px #888888 
9. 媒体查询：定义两套css，当浏览器的尺寸变化时会采用不同的属性 
10 请解释一下CSS3的flexbox（弹性盒布局模型）,以及适用场景？
该布局模型的目的是提供一种更加高效的方式来对容器中的条目进行布局、对齐和分配空间。在传统的布局方式中，block 布局是把块在垂直方向从上到下依次排列的；而 inline 布局则是在水平方向来排列。弹性盒布局并没有这样内在的方向限制，可以由开发人员自由操作。试用场景：弹性布局适合于移动前端开发，在Android和ios上也完美支持。
11 用纯CSS创建一个三角形的原理是什么？
首先，需要把元素的宽度、高度设为0。然后设置边框样式。
width : 0 ;
height : 0 ;
border -top : 40px solid transparent;
border -left : 40px solid transparent;
border -right : 40px solid transparent;
border -bottom : 40px solid #ff0000;
12 一个满屏品字布局如何设计?
第一种真正的品字：
1. 三块高宽是确定的； 
2. 上面那块用margin: 0 auto;居中； 
3. 下面两块用float或者inline-block不换行； 
4. 用margin调整位置使他们居中。 
第二种全屏的品字布局:上面的div设置成100%，下面的div分别宽50%，然后使用float或者inline使其不换行。
13 常见的兼容性问题？
1. 不同浏览器的标签默认的margin和padding不一样。*{margin:0;padding:0;} 
2. IE6双边距bug：块属性标签float后，又有横行的margin情况下，在IE6显示margin比设置的大。hack：display:inline;将其转化为行内属性。 
3. 渐进识别的方式，从总体中逐渐排除局部。首先，巧妙的使用“9”这一标记，将IE浏览器从所有情况中分离出来。接着，再次使用“+”将IE8和IE7、IE6分离开来，这样IE8已经独立识别。 { background -color :#f1ee18;/*所有识别*/ . background- color: #00deff\9; /*IE6、7、8识别*/ + background- color: #a200ff;/*IE6、7识别*/ _background -color :#1e0bd1;/*IE6识别*/ } 
4. 设置较小高度标签（一般小于10px），在IE6，IE7中高度超出自己设置高度。hack：给超出高度的标签设置overflow:hidden;或者设置行高line-height 小于你设置的高度。 
5. IE下，可以使用获取常规属性的方法来获取自定义属性,也可以使用getAttribute()获取自定义属性；Firefox下，只能使用getAttribute()获取自定义属性。解决方法:统一通过getAttribute()获取自定义属性。 
6. Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示,可通过加入 CSS 属性 -webkit-text-size-adjust: none; 解决。 
7. 超链接访问过后hover样式就不出现了，被点击访问过的超链接样式不再具有hover和active了。解决方法是改变CSS属性的排列顺序:L-V-H-A ( love hate ): a:link {} a:visited {} a:hover {} a:active {} 

14 为什么要初始化CSS样式
因为浏览器的兼容问题，不同浏览器对有些标签的默认值是不同的，如果没对CSS初始化往往会出现浏览器之间的页面显示差异。
15 absolute的containing block计算方式跟正常流有什么不同？
无论属于哪种，都要先找到其祖先元素中最近的 position 值不为 static 的元素，然后再判断：
1. 若此元素为 inline 元素，则 containing block 为能够包含这个元素生成的第一个和最后一个 inline box 的 padding box (除 margin, border 外的区域) 的最小矩形； 
2. 否则,则由这个祖先元素的 padding box 构成。 
如果都找不到，则为 initial containing block。
补充：
1. static(默认的)/relative：简单说就是它的父元素的内容框（即去掉padding的部分） 
2. absolute: 向上找最近的定位为absolute/relative的元素 
3. fixed: 它的containing block一律为根元素(html/body) 
16 CSS里的visibility属性有个collapse属性值？在不同浏览器下以后什么区别？
当一个元素的visibility属性被设置成collapse值后，对于一般的元素，它的表现跟hidden是一样的。
1. chrome中，使用collapse值和使用hidden没有区别。 
2. firefox，opera和IE，使用collapse值和使用display：none没有什么区别。 
17 display:none与visibility：hidden的区别？
display：none 不显示对应的元素，在文档布局中不再分配空间（回流+重绘）visibility：hidden 隐藏对应元素，在文档布局中仍保留原来的空间（重绘）
18 position跟display、overflow、float这些特性相互叠加后会怎么样？
display属性规定元素应该生成的框的类型；position属性规定元素的定位类型；float属性是一种布局方式，定义元素在哪个方向浮动。类似于优先级机制：position：absolute/fixed优先级最高，有他们在时，float不起作用，display值需要调整。float 或者absolute定位的元素，只能是块元素或表格。
19 对BFC规范(块级格式化上下文：block formatting context)的理解？
BFC规定了内部的Block Box如何布局。定位方案：
1. 内部的Box会在垂直方向上一个接一个放置。 
2. Box垂直方向的距离由margin决定，属于同一个BFC的两个相邻Box的margin会发生重叠。 
3. 每个元素的margin box 的左边，与包含块border box的左边相接触。 
4. BFC的区域不会与float box重叠。 
5. BFC是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。 
6. 计算BFC的高度时，浮动元素也会参与计算。 
满足下列条件之一就可触发BFC
1. 根元素，即html 
2. float的值不为none（默认） 
3. overflow的值不为visible（默认） 
4. display的值为inline-block、table-cell、table-caption 
5. position的值为absolute或fixed 
20 为什么会出现浮动和什么时候需要清除浮动？清除浮动的方式？
浮动元素碰到包含它的边框或者浮动元素的边框停留。由于浮动元素不在文档流中，所以文档流的块框表现得就像浮动框不存在一样。浮动元素会漂浮在文档流的块框上。浮动带来的问题：
1. 父元素的高度无法被撑开，影响与父元素同级的元素 
2. 与浮动元素同级的非浮动元素（内联元素）会跟随其后 
3. 若非第一个元素浮动，则该元素之前的元素也需要浮动，否则会影响页面显示的结构。 
清除浮动的方式：
1. 父级div定义height 
2. 最后一个浮动元素后加空div标签 并添加样式clear:both。 
3. 包含浮动元素的父标签添加样式overflow为hidden或auto。 
4. 父级div定义zoom 
21 上下margin重合的问题
在重合元素外包裹一层容器，并触发该容器生成一个BFC。例子：
< div class ="aside" ></div >
< div class ="text" >
    < div class ="main" ></div >
</ div>
<!--下面是 css代码-->
.aside {
             margin- bottom: 100px;   
             width: 100px;
             height: 150px;
             background: #f66;
         }
         .main {
             margin- top: 100px;
             height: 200px;
             background: #fcc;
         }
         .text {
             /*盒子main的外面包一个div，通过改变此div的属性使两个盒子分属于两个不同的BFC，以此来阻止margin重叠*/
             overflow: hidden;   //此时已经触发了BFC属性。
         }
22设置元素浮动后，该元素的display值是多少？
自动变成display:block
23 移动端的布局用过媒体查询吗？
通过媒体查询可以为不同大小和尺寸的媒体定义不同的css，适应相应的设备的显示。
1. <head>里边<link rel=”stylesheet” type=”text/css” href=”xxx.css” media=”only screen and (max-device-width:480px)”> 
2. CSS : @media only screen and (max-device-width:480px) {/css样式/} 
24 使用 CSS 预处理器吗？
Less sass
25 CSS优化、提高性能的方法有哪些？
1. 避免过度约束 
2. 避免后代选择符 
3. 避免链式选择符 
4. 使用紧凑的语法 
5. 避免不必要的命名空间 
6. 避免不必要的重复 
7. 最好使用表示语义的名字。一个好的类名应该是描述他是什么而不是像什么 
8. 避免！important，可以选择其他选择器 
9. 尽可能的精简规则，你可以合并不同类里的重复规则 
26 浏览器是怎样解析CSS选择器的？
CSS选择器的解析是从右向左解析的。若从左向右的匹配，发现不符合规则，需要进行回溯，会损失很多性能。若从右向左匹配，先找到所有的最右节点，对于每一个节点，向上寻找其父节点直到找到根元素或满足条件的匹配规则，则结束这个分支的遍历。两种匹配规则的性能差别很大，是因为从右向左的匹配在第一步就筛选掉了大量的不符合条件的最右节点（叶子节点），而从左向右的匹配规则的性能都浪费在了失败的查找上面。而在 CSS 解析完毕后，需要将解析的结果与 DOM Tree 的内容一起进行分析建立一棵 Render Tree，最终用来进行绘图。在建立 Render Tree 时（WebKit 中的「Attachment」过程），浏览器就要为每个 DOM Tree 中的元素根据 CSS 的解析结果（Style Rules）来确定生成怎样的 Render Tree。
27 在网页中的应该使用奇数还是偶数的字体？为什么呢？
使用偶数字体。偶数字号相对更容易和 web 设计的其他部分构成比例关系。Windows 自带的点阵宋体（中易宋体）从 Vista 开始只提供 12、14、16 px 这三个大小的点阵，而 13、15、17 px时用的是小一号的点。（即每个字占的空间大了 1 px，但点阵没变），于是略显稀疏。
28 margin和padding分别适合什么场景使用？
何时使用margin：
1. 需要在border外侧添加空白 
2. 空白处不需要背景色 
3. 上下相连的两个盒子之间的空白，需要相互抵消时。 
何时使用padding：
1. 需要在border内侧添加空白 
2. 空白处需要背景颜色 
3. 上下相连的两个盒子的空白，希望为两者之和。 
兼容性的问题：在IE5 IE6中，为float的盒子指定margin时，左侧的margin可能会变成两倍的宽度。通过改变padding或者指定盒子的display：inline解决。
29 元素竖向的百分比设定是相对于容器的高度吗？
当按百分比设定一个元素的宽度时，它是相对于父容器的宽度计算的，但是，对于一些表示竖向距离的属性，例如 padding-top , padding-bottom , margin-top , margin-bottom 等，当按百分比设定它们时，依据的也是父容器的宽度，而不是高度。
30 全屏滚动的原理是什么？用到了CSS的哪些属性？
1. 原理：有点类似于轮播，整体的元素一直排列下去，假设有5个需要展示的全屏页面，那么高度是500%，只是展示100%，剩下的可以通过transform进行y轴定位，也可以通过margin-top实现 
2. overflow：hidden；transition：all 1000ms ease； 
31 什么是响应式设计？响应式设计的基本原理是什么？如何兼容低版本的IE？
响应式网站设计(Responsive Web design)是一个网站能够兼容多个终端，而不是为每一个终端做一个特定的版本。基本原理是通过媒体查询检测不同的设备屏幕尺寸做处理。页面头部必须有meta声明的viewport。
<meta name="’viewport’" content= "”width=device-width," initial -scale= "1." maximum -scale= "1,user-scalable=no ”"/>
32 视差滚动效果？
视差滚动（Parallax Scrolling）通过在网页向下滚动的时候，控制背景的移动速度比前景的移动速度慢来创建出令人惊叹的3D效果。
1. CSS3实现优点：开发时间短、性能和开发效率比较好，缺点是不能兼容到低版本的浏览器 
2. jQuery实现通过控制不同层滚动速度，计算每一层的时间，控制滚动效果。优点：能兼容到各个版本的，效果可控性好缺点：开发起来对制作者要求高 
3. 插件实现方式例如：parallax-scrolling，兼容性十分好 
33 ::before 和 :after中双冒号和单冒号有什么区别？解释一下这2个伪元素的作用
1. 单冒号(:)用于CSS3伪类，双冒号(::)用于CSS3伪元素。 
2. ::before就是以一个子元素的存在，定义在元素主体内容之前的一个伪元素。并不存在于dom之中，只存在在页面之中。 
:before 和 :after 这两个伪元素，是在CSS2.1里新出现的。起初，伪元素的前缀使用的是单冒号语法，但随着Web的进化，在CSS3的规范里，伪元素的语法被修改成使用双冒号，成为::before ::after
34 你对line-height是如何理解的？
行高是指一行文字的高度，具体说是两行文字间基线的距离。CSS中起高度作用的是height和line-height，没有定义height属性，最终其表现作用一定是line-height。单行文本垂直居中：把line-height值设置为height一样大小的值可以实现单行文字的垂直居中，其实也可以把height删除。
多行文本垂直居中：需要设置display属性为inline-block。
35 怎么让Chrome支持小于12px 的文字？
p{ font-size :10px; -webkit- transform:scale (0.8);} //0.8是缩放比例
36 让页面里的字体变清晰，变细用CSS怎么做？

-webkit-font-smoothing在window系统下没有起作用，但是在IOS设备上起作用-webkit-font-smoothing：antialiased是最佳的，灰度平滑。
37 position:fixed;在android下无效怎么处理？
< meta name= "viewport" content ="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no" />
38 如果需要手动写动画，你认为最小时间间隔是多久，为什么？
多数显示器默认频率是60Hz，即1秒刷新60次，所以理论上最小间隔为1/60＊1000ms ＝ 16.7ms。
39 li与li之间有看不见的空白间隔是什么原因引起的？有什么解决办法？
行框的排列会受到中间空白（回车空格）等的影响，因为空格也属于字符,这些空白也会被应用样式，占据空间，所以会有间隔，把字符大小设为0，就没有空格了。解决方法：
1. 可以将<li>代码全部写在一排 
2. 浮动li中float：left 
3. 在ul中用font-size：0（谷歌不支持）；可以使用letter-space：-3px 
40 display:inline-block 什么时候会显示间隙？
1. 有空格时候会有间隙 解决：移除空格 
2. margin正值的时候 解决：margin使用负值 
3. 使用font-size时候 解决：font-size:0、letter-spacing、word-spacing 
41 有一个高度自适应的div，里面有两个div，一个高度100px，希望另一个填满剩下的高度
外层div使用position：relative；高度要求自适应的div使用position: absolute; top: 100px; bottom: 0; left: 0
42 png、jpg、gif 这些图片格式解释一下，分别什么时候用。有没有了解过webp？
1. png是便携式网络图片（Portable Network Graphics）是一种无损数据压缩位图文件格式.优点是：压缩比高，色彩好。 大多数地方都可以用。 
2. jpg是一种针对相片使用的一种失真压缩方法，是一种破坏性的压缩，在色调及颜色平滑变化做的不错。在www上，被用来储存和传输照片的格式。 
3. gif是一种位图文件格式，以8位色重现真色彩的图像。可以实现动画效果. 
4. webp格式是谷歌在2010年推出的图片格式，压缩率只有jpg的2/3，大小比png小了45%。缺点是压缩的时间更久了，兼容性不好，目前谷歌和opera支持。 
43 style标签写在body后与body前有什么区别？
页面加载自上而下 当然是先加载样式。写在body标签后由于浏览器以逐行方式对HTML文档进行解析，当解析到写在尾部的样式表（外联或写在style标签）会导致浏览器停止之前的渲染，等待加载且解析样式表完成之后重新渲染，在windows的IE下可能会出现FOUC现象（即样式失效导致的页面闪烁问题）
44 CSS属性overflow属性定义溢出元素内容区的内容会如何处理?
参数是scroll时候，必会出现滚动条。参数是auto时候，子元素内容大于父元素时出现滚动条。参数是visible时候，溢出的内容出现在父元素之外。参数是hidden时候，溢出隐藏。
45 阐述一下CSS Sprites
将一个页面涉及到的所有图片都包含到一张大图中去，然后利用CSS的 background-image，background- repeat，background-position 的组合进行背景定位。利用CSS Sprites能很好地减少网页的http请求，从而大大的提高页面的性能；CSS Sprites能减少图片的字节。

觉得本文对你有帮助？请分享给更多人

46.CSS渐变效果实现
background: linear-gradient(#ed6d06, transparent);
background: linear-gradient(rgba(0,0,0,0.32),transparent);
```

## 浏览器
https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/
```
从浏览器地址栏输入url到显示页面的步骤(以HTTP为例)
1. 在浏览器地址栏输入URL
2. 浏览器查看缓存，如果请求资源在缓存中并且新鲜，跳转到转码步骤
    * 如果资源未缓存，发起新请求
    * 如果已缓存，检验是否足够新鲜，足够新鲜直接提供给客户端，否则与服务器进行验证。
    * 检验新鲜通常有两个HTTP头进行控制Expires和Cache-Control：
        * HTTP1.0提供Expires，值为一个绝对时间表示缓存新鲜日期
        * HTTP1.1增加了Cache-Control: max-age=,值为以秒为单位的最大新鲜时间
3. 浏览器解析URL获取协议，主机，端口，path
4. 浏览器组装一个HTTP（GET）请求报文
5. 浏览器获取主机ip地址，过程如下：
    * 浏览器缓存
    * 本机缓存
    * hosts文件
    * 路由器缓存
    * ISP DNS缓存
    * DNS递归查询（可能存在负载均衡导致每次IP不一样）
6. 打开一个socket与目标IP地址，端口建立TCP链接，三次握手如下：
    * 客户端发送一个TCP的SYN=1，Seq=X的包到服务器端口
    * 服务器发回SYN=1， ACK=X+1， Seq=Y的响应包
    * 客户端发送ACK=Y+1， Seq=Z
7. TCP链接建立后发送HTTP请求
8. 服务器接受请求并解析，将请求转发到服务程序，如虚拟主机使用HTTP Host头部判断请求的服务程序
9. 服务器检查HTTP请求头是否包含缓存验证信息如果验证缓存新鲜，返回304等对应状态码
10. 处理程序读取完整请求并准备HTTP响应，可能需要查询数据库等操作
11. 服务器将响应报文通过TCP连接发送回浏览器
12. 浏览器接收HTTP响应，然后根据情况选择关闭TCP连接或者保留重用，关闭TCP连接的四次握手如下：
    * 主动方发送Fin=1， Ack=Z， Seq= X报文
    * 被动方发送ACK=X+1， Seq=Z报文
    * 被动方发送Fin=1， ACK=X， Seq=Y报文
    * 主动方发送ACK=Y， Seq=X报文
13. 浏览器检查响应状态吗：是否为1XX，3XX， 4XX， 5XX，这些情况处理与2XX不同
14. 如果资源可缓存，进行缓存
15. 对响应进行解码（例如gzip压缩）
16. 根据资源类型决定如何处理（假设资源为HTML文档）
17. 解析HTML文档，构件DOM树，下载资源，构造CSSOM树，执行js脚本，这些操作没有严格的先后顺序，以下分别解释
18. 构建DOM树：
    * Tokenizing：根据HTML规范将字符流解析为标记
    * Lexing：词法分析将标记转换为对象并定义属性和规则
    * DOM construction：根据HTML标记关系将对象组成DOM树
19. 解析过程中遇到图片、样式表、js文件，启动下载
20. 构建CSSOM树：
    * Tokenizing：字符流转换为标记流
    * Node：根据标记创建节点
    * CSSOM：节点创建CSSOM树
21. 根据DOM树和CSSOM树构建渲染树:
    * 从DOM树的根节点遍历所有可见节点，不可见节点包括：1）script,meta这样本身不可见的标签。2)被css隐藏的节点，如display: none
    * 对每一个可见节点，找到恰当的CSSOM规则并应用
    * 发布可视节点的内容和计算样式
22. js解析如下：
    * 浏览器创建Document对象并解析HTML，将解析到的元素和文本节点添加到文档中，此时document.readystate为loading
    * HTML解析器遇到没有async和defer的script时，将他们添加到文档中，然后执行行内或外部脚本。这些脚本会同步执行，并且在脚本下载和执行时解析器会暂停。这样就可以用document.write()把文本插入到输入流中。同步脚本经常简单定义函数和注册事件处理程序，他们可以遍历和操作script和他们之前的文档内容
    * 当解析器遇到设置了async属性的script时，开始下载脚本并继续解析文档。脚本会在它下载完成后尽快执行，但是解析器不会停下来等它下载。异步脚本禁止使用document.write()，它们可以访问自己script和之前的文档元素
    * 当文档完成解析，document.readState变成interactive
    * 所有defer脚本会按照在文档出现的顺序执行，延迟脚本能访问完整文档树，禁止使用document.write()
    * 浏览器在Document对象上触发DOMContentLoaded事件
    * 此时文档完全解析完成，浏览器可能还在等待如图片等内容加载，等这些内容完成载入并且所有异步脚本完成载入和执行，document.readState变为complete,window触发load事件
23. 显示页面（HTML解析过程中会逐步显示页面）


由上所述，我们可以得出以下结论:
css加载不会阻塞DOM树的解析
css加载会阻塞DOM树的渲染
css加载会阻塞后面js语句的执行
因此，为了避免让用户看到长时间的白屏时间，我们应该尽可能的提高css加载速度，比如可以使用以下几种方法:
使用CDN(因为CDN会根据你的网络状况，替你挑选最近的一个具有缓存内容的节点为你提供资源，因此可以减少加载时间)
对css进行压缩(可以用很多打包工具，比如webpack,gulp等，也可以通过开启gzip压缩)
合理的使用缓存(设置cache-control,expires,以及E-tag都是不错的，不过要注意一个问题，就是文件更新后，你要避免缓存而带来的影响。其中一个解决防范是在文件名字后面加一个版本号)
减少http请求数，将多个css文件合并，或者是干脆直接写成内联样式(内联样式的一个缺点就是不能缓存)

```
## 缓存

```
一、缓存的作用
重用已获取的资源，减少延迟与网络阻塞，进而减少显示某个资源所用的时间，借助 HTTP 缓存，Web 站点变得更具有响应性。

其实我们对于页面静态资源的要求就两点
1、静态资源加载速度
2、页面渲染速度

页面渲染速度建立在资源加载速度之上，但不同资源类型的加载顺序和时机也会对其产生影响，所以缓存的可操作空间非常大

二、缓存分类
image

整个系列只讨论浏览器（客户端）方面的缓存

三、缓存应该放在哪里？
在 Web 应用中使用缓存是一种改善响应时间和减少 CPU 使用的绝佳方式，但是，缓存应该放置在架构的哪个环节中呢？

这里不直接给答案（我不会告诉你是我给不出答案😂），通过分析的方式来引导大家，分析自己的项目的性能问题，性能瓶颈在哪？
是文件太大，还是请求数量太多？
重复的无效请求是否太多？
数据或者结果可以缓存吗？
这些数据、结果、文件的刷新率如何，容易失效吗？

这些问题，一千个项目有一千个答案，只有弄明白了缓存的核心原理，才能以不变应万变，信手沾来。

四、缓存的一些应用场景
1、每次都加载某个同样的静态文件 => 浪费带宽，重复请求 => 让浏览器使用本地缓存（协商缓存，返回304）
2、协商缓存还是要和服务器通信啊 => 有网络请求，不太舒服，感觉很low => 强制浏览器使用本地强缓存（返回200）
3、缓存要更新啊，兄弟，网络请求都没了，我咋知道啥时候要更新？=> 让请求（header加上ETag）或者url的修改与文件内容关联（文件名加哈希值）=> 开心，感觉自己很牛逼
4、CTO大佬说，我们买了阿里还是腾讯的CDN，几百G呢，用起来啊 => 把静态资源和动态网页分集群部署，静态资源部署到CDN节点上，网页中引用的资源变成对应的部署路径 => html中的资源引用和CDN上的静态资源对应的url地址联系起来了 => 问题来了，更新的时候先上线页面，还是先上线静态资源？（蠢，等到半天三四点啊，用户都睡了，随便你先上哪个）
5、老板说：我们的产品将来是国际化的，不存在所谓的半夜三点 => GG，咋办？=> 用非覆盖式发布啊，用文件的摘要信息来对资源文件进行重命名，把摘要信息放到资源文件发布路径中，这样，内容有修改的资源就变成了一个新的文件发布到线上，不会覆盖已有的资源文件。上线过程中，先全量部署静态资源，再灰度部署页面

五、各类缓存技术优缺点
1、cookie
优点：对于传输部分少量不敏感数据，非常简明有效
缺点：容量小（4K），不安全（cookie被拦截，很可能暴露session）；原生接口不够友好，需要自己封装；需要指定作用域，不可以跨域调用

2、Web Storage
容量稍大一点（5M），localStorage可做持久化数据存储
支持事件通知机制，可以将数据更新的通知发送给监听者
缺点：本地储存数据都容易被篡改，容易受到XSS攻击

缓存读取需要依靠js的执行，所以前提条件就是能够读取到html及js代码段，其次文件的版本更新控制会带来更多的代码层面的维护成本，所以LocalStorage更适合关键的业务数据而非静态资源

Cookie的作用是与服务器进行交互，作为HTTP规范的一部分而存在 ，而Web Storage仅仅是为了在本地“存储”数据而生

3、indexDB
IndexedDb提供了一个结构化的、事务型的、高性能的NoSQL类型的数据库，包含了一组同步/异步API，这部分不好判断优缺点，主要看使用者。

4、Manifest（已经被web标准废除）
优点

可以离线运行
可以减少资源请求
可以更新资源
缺点

更新的资源，需要二次刷新才会被页面采用
不支持增量更新，只有manifest发生变化，所有资源全部重新下载一次
缺乏足够容错机制，当清单中任意资源文件出现加载异常，都会导致整个manifest策略运行异常
Manifest被移除是技术发展的必然，请拥抱Service Worker吧

5、PWA(Service Worker)
这位目前是最炙手可热的缓存明星，是官方建议替代Application Cache（Manifest）的方案
作为一个独立的线程，是一段在后台运行的脚本，可使web app也具有类似原生App的离线使用、消息推送、后台自动更新等能力

目前有三个限制（不能明说是缺点）

不能访问 DOM
不能使用同步 API
需要HTTPS协议
六、缓存实践（视项目而定，不要死板）
1、大公司静态资源优化方案
配置超长时间的本地缓存 —— 节省带宽，提高性能
采用内容摘要作为缓存更新依据 —— 精确的缓存控制
静态资源CDN部署 —— 优化网络请求
更资源发布路径实现非覆盖式发布 —— 平滑升级
2、利用浏览器缓存机制
对于某些不需要缓存的资源，可以使用 Cache-control: no-store ，表示该资源不需要缓存
对于频繁变动的资源（比如经常需要刷新的首页，资讯论坛新闻类），可以使用 Cache-Control: no-cache 并配合 ETag 使用，表示该资源已被缓存，但是每次都会发送请求询问资源是否更新。
对于代码文件来说，通常使用 Cache-Control: max-age=31536000 并配合策略缓存使用，然后对文件进行指纹处理，一旦文件名变动就会立刻下载新的文件。
3、静态资源文件通过Service Worker进行缓存控制和离线化加载
```
