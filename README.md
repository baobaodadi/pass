# 总结
## ES5
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
##### 什么是ES6，什么是Shims/Polyfills
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

## 浏览器

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