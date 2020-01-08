# 问题与简答

## WEB篇

### 请列举几个常见的 `meta` 元素

- `<meta name="keywords" content="" >` //向搜索引擎说明你网页的关键词
- `<meta name="description" content="" >` //告诉搜索引擎你站点的主要内容
- `<meta name="author" content="你的姓名" >` //告诉搜索引擎你站点的作者
- `<meta http-equv="Content-Type" content="text/html;charset=utf-8" >` //指定字符集
- `<meta http-equv="refresh" content="n;url=" >` //定时让网页在指定的时间n内跳转
- `<meta http-equv="expires" content="Mon,12 Mqy 2019 11:06:10 GMT" >` //可以用于设定网页的到期时间，一旦过期则必须到服务器上重新调用
- `<meta http-equv="pragma" content="no-cache" >` //禁止缓存

### JavaScript的内置对象有哪些

- String字符串对象：String.length
- Date日期对象：Date.getYear()
- Math数学对象：Math.random()
- Array对象：Array.pop()，Array.push()
- Dom对象，Bom对象

### 解释js闭包的意思

两个函数彼此嵌套，内部函数可以访问外部函数的参数和变量，外部函数的参数和变量不会被垃圾回收机制回收，并且跟返回的内部函数形成了一个“环境包”，这个包属于内部函数，所以叫闭包。好处：变量可以长期存在于内存中，避免污染全局变量。

### JavaScript中包含哪些基本数据类型

- 原始类型：Number，String，Boolean，Null，Undefined
- 对象类型：全局对象，数组，函数

### 为什么把 JavaScript 文件放在 Html 底部

脚本会阻塞页面其他资源的下载，因此推荐将所有`<script>`标签尽可能放到`<body>`标签的底部，以尽量减少对整个页面下载的影响

### setTimeout 和 setInterval 的区别

setTimeout表示间隔一段时间之后执行一次调用，而setInterval则是每间隔一段时间循环调用，直至clearInterval结束。 内存方面，setTimeout只需要进入一次队列，不会造成内存溢出，setInterval因为不计算代码执行时间，有可能同时执行多次代码， 导致内存溢出。

### 如何实现 ajax 请求

通过实例化一个XMLHttpRequest对象得到一个实例，调用实例的open方法为这次 ajax请求设定相应的http方法、相应的地址和以及是否异步，当然大多数情况下我们都是选异步， 以异步为例，之后调用send方法ajax请求，这个方法可以设定需要发送的报文主体，然后通过 监听readystatechange事件，通过这个实例的readyState属性来判断这个ajax请求的状态，其中分为0,1,2,3,4这四种 状态，当状态为4的时候也就是接收数据完成的时候，这时候可以通过实例的status属性判断这个请求是否成功

```javascript
var xhr = new XMLHttpRequest();
xhr.open('get', 'aabb.php', true);
xhr.send(null);
xhr.onreadystatechange = function() {
  if(xhr.readyState==4) {
    if(xhr.status==200) {
      console.log(xhr.responseText);
    }
  }
}
```

### 对 JavaScript 原型的理解

我们知道在es6之前，js没有类和继承的概念，js是通过原型来实现继承的。在js中一个构造函数默认自带有一个prototype属性， 这个的属性值是一个对象，同时这个prototype对象自带有一个constructor属性，这个属性指向这个构造函数，同时每一个实例 都有一个__proto__属性指向这个prototype对象，我们可以将这个叫做隐式原型，我们在使用一个实例的方法的时候，会先检查 这个实例中是否有这个方法，没有则会继续向上查找这个prototype对象是否有这个方法，刚刚我们说到prototype是一个对象， 那么也即是说这个是一个对象的实例，那么这个对象同样也会有一个__proto__属性指向对象的prototype对象

### 对 JavaScript 模块化的理解

在ES6出现之前，js没有标准的模块化概念，这也就造成了js多人写作开发容易造成全局污染的情况，以前我们可能会采用立即执行 函数、对象等方式来尽量减少变量这种情况，后面社区为了解决这个问题陆续提出了AMD规范和CMD规范，这里不同于Node.js的 CommonJS的原因在于服务端所有的模块都是存在于硬盘中的，加载和读取几乎是不需要时间的，而浏览器端因为加载速度取决于网速， 因此需要采用异步加载，AMD规范中使用define来定义一个模块，使用require方法来加载一个模块，现在ES6也推出了标准的模块 加载方案，通过export和import来导出和导入模块。

### 什么是 Ajax？Ajax 的原理是什么？Ajax 的核心技术是什么？Ajax 的优缺点是什么？

Ajax 是 Asynchronous JavaScript and XML 的缩写，是 JavaScript、XML、CSS、DOM 等 多个技术的组合。Ajax 的工作原理是一个页面的指定位置可以加载另一个页面所有的输出内容，这样就 实现了一个静态页面也能获取到数据库中的返回数据信息了。所以 Ajax 技术实现了一个静 态网页在不刷新整个页面的情况下与服务器通信，减少了用户等待时间，同时也从而降低了 网络流量，增强了客户体验的友好程度。Ajax 的核心技术是 XMLHttpRequest，它是 JavaScript 中的一个对象。

Ajax 的优点是：

- 减轻了服务器端负担，将一部分以前由服务器负担的工作转移到客户端执行，利用 客户端闲置的资源进行处理；


- 在只局部刷新的情况下更新页面，增加了页面反应速度，使用户体验更友好。

Ajax 的缺点：

- 不利于 SEO 推广优化，因为搜索引擎无法直接访问到 Ajax 请求的内容

### SESSION 与 COOKIE的区别是什么，请从协议，产生的原因与作用说明

- http无状态协议，不能区分用户是否是从同一个网站上来的，同一个用户请求不同的页面不能看做是同一个用户。


- SESSION存储在服务器端，COOKIE保存在客户端。Session比较安全，cookie用某些手段可以修改，不安全。Session依赖于cookie进行传递。


- 禁用cookie后，session不能正常使用。**Session的缺点：**保存在服务器端，每次读取都从服务器进行读取，对服务器有资源消耗。Session保存在服务器端的文件或数据库中，默认保存在文件中，文件路径由php配置文件的session.save_path指定。Session文件是公有的。

### 表单中 get与post提交方法的区别

- get是把参数数据队列加到提交表单的ACTION属性所指的URL中，值和表单内各个字段一一对应，在URL中可以看到。post是通过HTTP post机制，将表单内各个字段与其内容放置在HTML HEADER内一起传送到ACTION属性所指的URL地址。用户看不到这个过程。


- 对于get方式，服务器端用Request.QueryString获取变量的值，对于post方式，服务器端用Request.Form获取提交的数据。


- get传送的数据量较小，不能大于2KB。post传送的数据量较大，一般被默认为不受限制。但理论上，IIS4中最大量为80KB，IIS5中为100KB。get安全性非常低，post安全性较高

### javascript能否定义二维数组，如果不能你如何解决

javascript不支持二维数组定义，可以用arr[0] = new array()来解决。

### Cookie 读写

```js
document.cookie = "name=oeschger";
document.cookie = "favorite_food=tripe";
alert(document.cookie);
// 显示: name=oeschger;favorite_food=tripe
```

```js
document.cookie = "test1=Hello";
document.cookie = "test2=World";
var myCookie = document.cookie.replace(/(?:(?:^|.*;\s*)test2\s*\=\s*([^;]*).*$)|^.*$/, "$1");
alert(myCookie);
// 显示: World
```

### 同源策略是什么

同源策略是指只有具有相同源的页面才能够共享数据，比如cookie，同源是指页面具有相同的协议、域名、端口号，有一项不同就不是同源。 有同源策略能够保证web网页的安全性。

### link 与 @import 的区别

- link 是 HTML 方式， @import 是 CSS 方式


- link 最大限度支持并行下载，@import 过多嵌套导致串行下载，出现FOUC


- link 可以通过 rel="alternate stylesheet"指定候选样式


- 浏览器对 link 支持早于 @import，可以使用 @import 对老浏览器隐藏样式


- @import 必须在样式规则之前，可以在 css 文件中引用其他文件

总体来说：link 优于 @import

### 请介绍Session的原理

因为HTTP是无状态的，所以一次请求完成后客户端和服务端就不再有任何关系了，谁也不认识谁。但由于一些需要（如保持登录状态等），必须让服务端和客户端保持联系，session ID就成了这种联系的媒介了。当用户第一次访问站点时，PHP会用session_start()函数为用户创建一个session ID，这就是针对这个用户的唯一标识，每一个访问的用户都会得到一个自己独有的session ID，这个session ID会存放在响应头里的cookie中，之后发送给客户端。这样客户端就会拥有一个该站点给他的session ID。当用户第二次访问该站点时，浏览器会带着本地存放的cookie(里面存有上次得到的session ID)随着请求一起发送到服务器，服务端接到请求后会检测是否有session ID，如果有就会找到响应的session文件，把其中的信息读取出来；如果没有就跟第一次一样再创建个新的。

#### session共享问题解决方案

- 客户端Cookie保存，以cookie加密的方式保存在客户端，每次session信息被写在客户端，然后经浏览器再次提交到服务器。


- 服务器间Session同步，使用主-从服务器的架构，当用户在主服务器上登录后，通过脚本或者守护进程的方式，将session信息传递到各个从服务器中


- 使用集群统一管理Session，当应用系统需要session信息的时候直接到session群集服务器上读取，目前大多都是使用Memcache来对Session进行存储。


- 把Session持久化到数据库，目前采用这种方案时所使用的数据库一般为mysql。