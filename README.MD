## 每日一题

在这里记录着每天自己遇到的一道印象深刻的前端问题。鞭挞自己不断前行，共同学习。

### **2019/12/16**⌚️

- JSON.parse(JSON.stringify(obj))实现深度克隆的缺点是什么？

    <details >
          <summary>点击</summary>
          <ul>
              <li>他无法实现对函数 、RegExp 等特殊对象的克隆</li>
              <li>会抛弃对象的 constructor,所有的构造函数会指向 Object</li>
              <li>对象有循环引用,会报错</li>
          </ul>
      </details>

<hr>

### **2019/12/17**⌚️

- PHP如何操作数据库增加数据表中的数据？

  <details >
        <summary>点击</summary>
        <ul>
            <li>首先需要创建mysql命令的字符串：$str = 'INSERT stu (user,sex,age) VALUES("小二","男",20)';</li>
            <li>字符串的格式务必要注意，VALUES后的字符必须加“”，哪怕是用$u变量去拼接，也需要用""把变量包裹才可以</li>
            <li>$q = $link->query($str);发送mysql语句，执行对应的操作</li>
        </ul>
    </details>

<hr>

### **2019/12/18**⌚️

- 如何实现JSONP

  <details >
        <summary>点击</summary>

  #### JS代码

  ```js
  var url = "http://localhost/myown/jsonp/jsonp2.php";
  document.onclick = function () {
      jsonp(url, (res) => {
          console.log(res);
      }, {
          cb: "qwe",
          cbname: "cb",
          user: "root",
          pass: "root"
      })
  }
  
  function jsonp(url, callback, obj) {
      var str = "";
      var script = document.createElement("script");
      for (var i in obj) {
          str += `${i}=${obj[i]}&`;
      }
      url = url + "?" + str + "__retr0__=" + new Date().getTime();
      script.src = url;
      document.body.appendChild(script);
      window[obj[obj.cbname]] = function (res) {
              callback(res);
      }
      script.remove();
  }
  ```

  #### PHP代码

  ```php
  <?php
  $u = $_GET["user"];
  $p = $_GET["pass"];
  $cb = $_GET["cb"];
  $data = "这是JSONP接受到的数据" . $u . "------" . $p;
  echo "$cb('" . $data . "')";
  ?>
  ```

  

    </details>

<hr>

### **2019/12/19**⌚️

- mysql如何对数据进行增删改查

<details >
<summary>点击</summary>
<ul>
<li>INSERT 表名(字段名1，字段名2) VALUES(val1,val2)</li>
<li>DELETE FROM 表名 WHERE 主键 = val </li>
<li>UPDATE 表名 SET 字段1 WHERE 主键 = val</li>
<li>SELECT * FROM 表名</li>      

</ul>
</details>

  <hr>

### **2019/12/20**⌚️

- cookies中的expires的作用

<details >
<summary>点击</summary>
<ul>
<li>指定了cookie的生存期，默认情况下cookie是暂时存在的，他们存储的值只在浏览器会话期间存在，当用户退出浏览器后这些值也会丢失，如果想让cookie存在一段时间，就要为expires属性设置为未来的一个用毫秒数表示的过期日期或时间点，expires默认为设置的expires的当前时间。现在已经被max-age属性所取代，max-age用秒来设置cookie的生存期。</li>
<li>如果max-age属性为正数，则表示该cookie会在max-age秒之后自动失效。浏览器会将max-age为正数的cookie持久化，即写到对应的cookie文件中。无论客户关闭了浏览器还是电脑，只要还在max-age秒之前，登录网站时该cookie仍然有效。</li>
<li>如果max-age为负数，则表示该cookie仅在本浏览器窗口以及本窗口打开的子窗口内有效，关闭窗口后该cookie即失效。max-age为负数的Cookie，为临时性cookie，不会被持久化，不会被写到cookie文件中。cookie信息保存在浏览器内存中，因此关闭浏览器该cookie就消失了。cookie默认的max-age值为-1。</li>

<li>	如果max-age为0，则表示删除该cookie。cookie机制没有提供删除cookie的方法，因此通过设置该cookie即时失效实现删除cookie的效果。失效的Cookie会被浏览器从cookie文件或者内存中删除。

如果不设置expires或者max-age这个cookie默认是Session的，也就是关闭浏览器该cookie就消失了。</li>

​      </ul>
</details>

<hr>

### **2019/12/21**⌚️

- mysql如何取消主键的设置

<details >
<summary>点击</summary>
<ul>
<li>alter table class drop primary key;</li>
<li>alter table class modify id int(11),drop primary key;//将class表中的id 重置为普通列 </li>

</ul>
</details>

<hr>

### **2019/12/22**⌚️

- windos身上的子对象有哪些

<details >
<summary>点击</summary>
<ul>
<li>window.history</li>
<li>window.frames</li>
<li>window.screen</li>
<li>window.navigator</li>
<li>window.location</li>
<li>window.document</li>

</ul>
</details>

<hr>

### **2019/12/23**⌚️

- localStorage的方法有哪些

<details >
<summary>点击</summary>
<ul>
<li>localStorage.setItem(key,val)</li>
<li>localStorage.getItem(key)</li>
<li>localStorage.removeItem(key)</li>
<li>localStorage.clear()</li>

</ul>
</details>

<hr>

### **2019/12/24**⌚️

- 如何设置一条３天之后过期的在根目录下的cookie

<details >
<summary>点击</summary>

```js
var d = new Date();
d.setDate(d.getDate()+3);
document.cookie = "user=admin;path=/;expires="+d;
```

</details>

<hr>

### **2019/12/25**⌚️

- 什么是发布订阅者模式

<details >
<summary>点击</summary>

1. 发布者（你）
2. 缓存列表（通讯录，你的朋友们相当于订阅了你的所有消息）
3. 发布消息的时候遍历缓存列表，依次触发里面存放的订阅者的回调函数（挨个打电话）
4. 另外，回调函数中还可以添加很多参数，，订阅者可以接收这些参数，比如你会告诉他们婚礼时间，地点等，订阅者收到消息后可以进行各自的处理。

```js
let yourMsg = {};
yourMsg.peopleList = [];
yourMsg.listen = function (fn) {
    this.peopleList.push(fn);
}
yourMsg.triger = function () {
    for(var i = 0,fn;fn=this.peopleList[i++];){
        fn.apply(this,arguments);
    }
}

yourMsg.listen(function (name) {
    console.log(`${name}收到了你的消息`);
})
yourMsg.listen(function (name) {
    console.log('哈哈');
})

yourMsg.triger('张三');
yourMsg.triger('李四');
```

![img](https://user-gold-cdn.xitu.io/2018/2/24/161c6c2aed446eec?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

- 以上就是一个简单的发布-订阅的实现，但是我们会发现订阅者会收到发布者发布的每一条信息，如果李四比较阴暗，不想听到你结婚的消息，只想听到你的坏消息，比如你被开除了，他就心里高兴。这时候我们就需要加一个key，让订阅者只订阅自己感兴趣的消息。

```js
let yourMsg = {};
yourMsg.peopleList ={};
yourMsg.listen = function (key,fn) {
    if (!this.peopleList[key]) { //如果没有订阅过此类消息，创建一个缓存列表
        this.peopleList[key] = [];
    }
    this.peopleList[key].push(fn);
}
yourMsg.triger = function () {
    let key = Array.prototype.shift.call(arguments);
    let fns = this.peopleList[key];
    if (!fns || fns.length == 0) {//没有订阅 则返回
        return false;
    }
    for(var i=0,fn;fn=fns[i++];){
        fn.apply(this,arguments);
    }
}

yourMsg.listen('marrgie',function (name) {
    console.log(`${name}想知道你结婚`);
})
yourMsg.listen('unemployment',function (name) {
    console.log(`${name}想知道你失业`);
})

yourMsg.triger('marrgie','张三');
yourMsg.triger('unemployment','李四');
```

![img](https://user-gold-cdn.xitu.io/2018/2/24/161c6ce98f1cede9?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

- 你需要发布消息，同样的所有的人都有朋友圈，也都需要发布消息，因此我们有必要把发布-订阅的功能提取出来，放在一个单独的对象内，谁需要谁去动态安装发布-订阅功能(installEvent函数实现了动态安装发布-订阅功能)。

```js
var event = {
    peopleList:[],
    listen:function (key,fn) {
        if (!this.peopleList[key]) { //如果没有订阅过此类消息，创建一个缓存列表
        this.peopleList[key] = [];
        }
        this.peopleList[key].push(fn)
    },
    trigger:function () {
         let key = Array.prototype.shift.call(arguments);
        let fns = this.peopleList[key];
        if (!fns || fns.length == 0) {//没有订阅 则返回
            return false;
        }
        for(var i=0,fn;fn=fns[i++];){
            fn.apply(this,arguments);
        }
    }
}

var installEvent  = function (obj) {
    for(var i in event){
        obj[i] = event[i];
    }
}

let yourMsg = {};
installEvent(yourMsg);
yourMsg.listen('marrgie',function (name) {
    console.log(`${name}想知道你结婚`);
})
yourMsg.listen('unemployment',function (name) {
    console.log(`${name}想知道你失业`);
})

yourMsg.trigger('marrgie','张三');
yourMsg.trigger('unemployment','李四');
```

- 有时间我们需要取消订阅的事件，比如李四是你的好朋友，但是因为一件事情，你俩闹掰了，你把他从你的通讯录中给删除掉了，这里我们给event增加一个remove方法；

```js
remove:function (key,fn) {
      var fns = this.clientList[key];
      if(!fns){
          return false;
      }  
      if(!fn){
          fns && (fns.length=0)
      }else{
          for (let index = 0; index < fns.length; index++) {
              const _fn = fns[index];
              if(_fn === fn){
                  fns.splice(index,1);
              }
          }
      }
    }
```

#### 发布-订阅的顺序探讨

我们通常所看到的都是先订阅再发布，但是必须要遵守这种顺序吗？答案是不一定的。如果发布者先发布一条消息，但是此时还没有订阅者订阅此消息，我们可以不让此消息消失于宇宙之中。就如同QQ离线消息一样，离线的消息被保存在服务器中，接收人下次登录之后，才会收到此消息。同样的，我们可以建立一个存放离线事件的堆栈，当事件发布的时候，如果此时还没有订阅者订阅这个事件，我们暂时把发布事件的动作包裹在一个函数里，这些包装函数会被存入堆栈中，等到有对象来订阅事件的时候，我们将遍历堆栈并依次执行这些包装函数，即重发里面的事件，不过离线事件的生命周期只有一次，就像qq未读消息只会提示你一次一样。

#### JavaScript实现发布-订阅模式的便利性

因为JavaScript有回调函数这个优势存在，我们写开发-订阅显得更简单一点。传统的发布-订阅比如Java通常会把订阅者自身当成引用传入发布者对象中，同时订阅者对象还需提供一个名为诸如update的方法，供发布者对象在合适的时候调用。下面代码用js模拟下传统的实现。

```js
function Dep() {
    this.subs = [];
}
Dep.prototype.addSub = function (sub) {
    this.subs.push(sub);
}
Dep.prototype.notify = function () {
    this.subs.forEach(sub=>sub.update());
}
function Watcher(fn) {
    this.fn = fn;
}
Watcher.prototype.update = function () {
     this.fn();
}

var dep = new Dep();
dep.addSub(new Watcher(function () {
    console.log('okokok');
}))
dep.notify();
```

#### 小结

- 发布-订阅的优势很明显，做到了时间上的解耦和对象之间的解耦，从架构上看，MVC，MVVM都少不了发布-订阅的参与，我们常用的Vue也是基于发布-订阅的，最近会抽时间写下vue的源码实现，同样的node中的EventEmitter也是发布订阅的，之前也手写过它的实现。
- 发布-订阅同时也是有缺点存在的，创建订阅者本身要消耗一定的时间和内存，而且当你订阅一个消息以后，可能此消息最后都未发生，但是这个订阅者会始终存在于内存中。如果程序中大量使用发布-订阅的话，也会使得程序跟踪bug变得困难。 

</details>

<hr>

### **2019/12/26**⌚️

- 请用jQuery实现一个图片的手风琴效果

<details >
<summary>点击</summary>

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <style>
        * {
            margin: 0;
            padding: 0;
            list-style: none;
        }

        .wrap {
            width: 1178px;
            height: 174px;
            overflow: hidden;
            position: relative;
            margin: 0 auto;

        }

        .wrap ul li {
            float: left;
            width: 210px;
            height: 174px;
            overflow: hidden;
        }

        .wrap ul {
            width: 2000px;
        }

        .wrap ul li img {
            width: 550px;
            height: 174px;
        }
    </style>
</head>

<body>

    <div class="wrap">
        <ul>
            <li style='width:550px'><img src="http://pic.shejiben.com/hot_sjb/377_8180.jpg?1462261126" alt=""></li>
            <li><img src="http://pic.shejiben.com/hot_sjb/377_8288.jpg?1464830033" alt=""></li>
            <li><img src="http://pic.shejiben.com/hot_sjb/377_8155.jpg?1460709517" alt=""></li>
            <li><img src="http://pic.shejiben.com/hot_sjb/377_7937.jpg?1456984280" alt=""></li>
        </ul>
    </div>
    <script src="https://lib.baomitu.com/jquery/1.12.4/jquery.js"></script>
    <script>
        $(".wrap").find("li").mouseover(function () {
            $(this).stop().animate({
                width: 550
            }).siblings().stop().animate({
                width: 210
            })
        })
    </script>
</body>

</html>
```

</details>

<hr>

### **2019/12/27**⌚️

- 说说jQuery的尺寸类方法

<details >
<summary>点击</summary>尺寸

### width()

> 设置或返回元素的宽度（不包括内边距、边框或外边距）

```js
$(".box").width();//获得宽度
$(".box").width(300);//设置宽度
```



### height()

> 设置或返回元素的高度（不包括内边距、边框或外边距）

```js
$(".box").height();//获得宽度
$(".box").height(300);//设置宽度
```



### innerWidth()

> 设置或返回元素的宽度（包括内边距）

```js
$(".box").innerWidth();//获得offsetWidth
$(".box").innerWidth(300);//值减去padding后设置给宽度
```



### innerHeight()

> 设置或返回元素的高度（包括内边距）

```js
$(".box").innerHeight();//获得offsetHeight
$(".box").innerHeight(300);//值减去padding后设置给高度
```



### outerWidth()

> 设置或返回元素的宽度（包括内边距,包括边框）

```js
$(".box").outerWidth();//获得clientWidth
$(".box").outerWidth(300);//值减去padding和border后设置给宽度
```



### outerHeight()

> 设置或返回元素的高度（包括内边距,包括边框）

```js
$(".box").outerHeight();//获得clientHeight
$(".box").outerHeight(300);//值减去padding和border后设置给高度
```



### offset()

> 设置或返回元素距离页面的left和top,返回一个对象(包含position+margin)

```js
console.log($(".box1").offset());       //position+margin
$(".box1").offset({left:100,top:100}) //值减去margin后设置给left和top
```



### position()

> 返回元素距离页面的left和top,返回一个对象(不margin)

```js
$(".box1").position().left;
$(".box1").position().top	;
```



### scrollTop()

> 设置或返回滚动条的高度

```js
$(".box1").scrollTop();
$(".box1").scrollTop(300);
```



</details>

<hr>

### **2019/12/28**⌚️

- 事件流的状态及含义

<details >
<summary>点击</summary>
<ul>
<li>事件冒泡：从内向外，依次触发所有父级的相同事件</li>
<li>事件捕获：从外向内，依次触发从最大的父级到目标的相同事件</li>
<li>目标事件：当前真正要触发的事件</li>

</ul>
</details>

<hr>

### **2019/12/29**⌚️

- cookie的特点

<details >
<summary>点击</summary>
<ul>
<li>文本</li>
<li>大小4K</li>
<li>不能跨域</li>
<li>条数50</li>
<li>时间限制</li>

</ul>
</details>

<hr>

### **2019/12/30**⌚️

- $.ajax()怎么实现超时报错

<details >
<summary>点击</summary>

```js
$.ajax({
    url:"https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su",
    dataType:"jsonp",
    jsonp:"cb",
    data:{
        wb:"html"
    },
    success:function(res,status,xhr){
		console.log(res); 
    	console.log(status);
    	console.log(xhr);
	},
    error:function(xhr,status,res){
    	console.log(xhr);
    	console.log(status);
    	console.log(res);
	}
	timeOut:100,//数值单位为毫秒，超时会执行error函数,status和res会输出timeOut字符串
})
```



</details>

<hr>

### **2019/12/31**⌚️

- 什么是端口

<details >
<summary>点击</summary>
<ul>
<li>端口的作用：`通过端口来区分出同一电脑内不同应用或者进程，从而实现一条物理网线(通过分组交换技术-比如internet)同时链接多个程`</li>
<li>端口号是一个 16位的 uint, 所以其范围为 1 to 65535 (对TCP来说, port 0 被保留，不能被使用. 对于UDP来说, source端的端口号是可选的， 为0时表示无端口).</li>
<li>`app.listen(3000)`，进程就被打标，电脑接收到的3000端口的网络消息就会被发送给我们启动的这个进程</li>

</ul>
</details>

<hr>

### **2020/01/01**⌚️

- node如何实现get/post请求返回数据

<details >
<summary>点击</summary>

```js
const http = require("http");
const fs = require("fs");
const url = require("url");
const querystring = require("querystring");
http.createServer((req,res)=>{
    if(req.url != "/favicon.ico"){
   		var pathname = url.parse(req.url).pathname;
        if(pathname === "/api"){
        	ajaxHandle(req,res)    
        }else{
            fsHandle(req,res)
        }
    }
}).listen("81","127.0.0.1",()=>{
    console.log("run server on http://127.0.0.1:81");
})
function ajaxHandle(req,res){
    let str = "";
    req.on("data",(data)=>{
        str +=data;
    })
    req.on("end",()=>{
        let data = str ? querystring(str):url.parse(req.url);
        res.write(JSON.parse(data));
        res.end();
    })
}
function fsHandle(req,res){
}
```



</details>

<hr>

### **2020/01/02**⌚️

- gulp如何自动开启服务器

<details >
<summary>点击</summary>

```js
const gulp = require("gulp");
const connect = require("gulp-connect");
function serverFn(){
    connect.server({
        root:"文件夹名"，
       	port:"端口名"
    })
}
```

</details>

<hr>

### **2020/01/03**⌚️

- 模块规范化的概念及优点

<details >
<summary>点击</summary>

<ul>
<li>模块规范化的概念：将项目的所有功能封装成独立的模块，模块之间按照一定的关系或者调用，实现整个项目的搭建</li>
<li>模块规范化的优点：封装，重用性强，耦合低，方便单独扩展</li>
</ul>

</details>

<hr>

### **2020/01/04**⌚️

- AMD模块的使用

<details >
<summary>点击</summary>

### require()

> 引入入口,引入模块
>
> require == requirejs //true

与传统的<script>标记相比，RequireJS采用了不同的方法来加载脚本。尽管它还可以快速运行并优化得很好，但主要目标是鼓励使用模块化代码。作为其一部分，它鼓励使用**模块ID**代替脚本标记的URL。

RequireJS加载相对于[baseUrl的](https://requirejs.org/docs/api.html#config-baseUrl)所有代码。通常，将baseUrl设置为与data-main属性中使用的脚本相同的目录，以使顶级脚本加载页面。该[数据主要属性](https://requirejs.org/docs/api.html#data-main)是一个特殊的属性，require.js将检查启动脚本加载。本示例将以**脚本**的baseUrl结尾：

```
<!--This sets the baseUrl to the "scripts" directory, and
    loads a script that will have a module ID of 'main'-->
<script data-main="scripts/main.js" src="scripts/require.js"></script>
```

或者，可以通过[RequireJS config](https://requirejs.org/docs/api.html#config)手动设置[baseUrl](https://requirejs.org/docs/api.html#config)。如果没有显式配置且未使用data-main，则默认的baseUrl是包含运行RequireJS的HTML页面的目录。

默认情况下，RequireJS还假定所有依赖项都是脚本，因此，它不会在模块ID上看到尾随的“ .js”后缀。在将模块ID转换为路径时，RequireJS将自动添加它。使用[path config](https://requirejs.org/docs/api.html#config-paths)，可以设置一组脚本的位置。与传统的<script>标记相比，所有这些功能都允许您为脚本使用较小的字符串。

有时您可能确实想直接引用脚本，而又不遵循“ baseUrl +路径”规则来查找脚本。如果模块ID具有以下特征之一，则该ID将不会通过“ baseUrl +路径”配置传递，而只会被视为与文档相关的常规URL：

- 以“ .js”结尾。
- 以“ /”开头。
- 包含URL协议，例如“ http：”或“ https：”。



### 参数

#### 数组

```js
["module/mA","module/mB"]
```

> 数组里存放多个小模块(JS的相对路径)
>
> 每个小模块之间是异步

#### 回调函数

```js
function(data1,data2){}
```

> 回调函数和外部代码之间是异步
>
> 回调函数和所有小模块之间是同步

### 引入同文件夹下的jS

```js
require(["module/mA.js", "module/mB.js"], function (a, b) {
    a.show(b.data);
    b.show(a.data);
})
```



### config(obj)

> 配置路径信息

obj包含2个键值对

基目录baseUrl：指定require在引入小模块时的起始路径

定义小模块的别名paths：起别名，在require引入模块时，可以通过别名引入模块

```js
require.config({
    baseUrl: "module4",
    paths: {
        jq: "../libs/jquery",
        a: "mA",
        b: "mB"
    }
})
```



### define()

> 暴露入口,定义模块

模块与传统脚本文件的不同之处在于，它定义了一个范围广泛的对象，可避免污染全局名称空间。它可以显式列出其依赖关系，并在不需要引用全局对象的情况下获取这些依赖关系的句柄，而是将依赖关系作为定义模块的函数的参数来接收。RequireJS中的[模块](http://www.adequatelygood.com/2010/3/JavaScript-Module-Pattern-In-Depth)是[Module Pattern](http://www.adequatelygood.com/2010/3/JavaScript-Module-Pattern-In-Depth)的扩展，其优点是不需要全局变量来引用其他模块。

模块的RequireJS语法允许它们以尽可能快的速度加载，即使顺序混乱也可以，但是以正确的依赖关系顺序进行评估，并且由于未创建全局变量，因此可以[在页面中加载模块的多个版本](https://requirejs.org/docs/api.html#multiversion)。

（如果您熟悉或正在使用CommonJS模块，那么也请参阅[CommonJS Notes](https://requirejs.org/docs/commonjs.html)以获取有关RequireJS模块格式如何映射到CommonJS模块的信息）。

磁盘上每个文件只能有**一个**模块定义。可以通过[优化工具](https://requirejs.org/docs/optimization.html)将模块分组为优化的包。

### 参数

#### 数组

> 当前定义的模块的依赖

```js
define(["libs/jQuery"],function (_) {
    //Do setup work here
	var a = $();
    function show(data){
        console.log(data);
    }
    return {
        data:a,
        fn:show
    }
});
```

​	如果当前定义的模块的`依赖没有`被放在define的第一个参数中被`提前加载`,那么在当前定义的模块中还想使用这个依赖的内容,那么千万`不要在当前模块`中直接`执行`,`封装成功能`,暴露出去,等待所有模块加载完成后再去执行。

#### 回调函数

### 简单名称/值对

如果模块没有任何依赖关系，而只是名称/值对的集合，则只需将对象文字传递给define（）：

```js
//Inside file my/shirt.js:
define({
    color: "black",
    size: "unisize"
});
```

### 定义函数

如果模块没有依赖项，但是需要使用函数来完成一些设置工作，则定义自己，然后将函数传递给define（）：

```js
//my/shirt.js now does setup work
//before returning its module definition.
define([],function () {
    //Do setup work here
	var a = "aaa";
    function show(data){
        console.log(data);
    }
    return {
        data:a,
        fn:show
    }
});
```



### 实例

### 模块A

```js
define([], function () {
    var a = "aaa";

    function fn(data) {
        console.log("A模块的是：" + data);
    }
    return {
        data: a,
        show: fn
    }
})
```



### 模块B

```js
define([], function () {
    var b = "bbb";

    function fn(data) {
        console.log("A模块的是：" + data);
    }
    return {
        data: b,
        show: fn
    }
})
```



### 主模块

```js
<script src="../../libs/require.js"></script>
<script>
    require(["module/mA.js", "module/mB.js"], function (a, b) {
        a.show(b.data);
        b.show(a.data);
    })
</script>
```

</details>

<hr>

### **2020/01/05**⌚️

- 如何手写一个promise功能

<details >
<summary>点击</summary>

```js
  // let promise = new _Promise((resolve, reject) => {
    //     //这里放入我们要执行的函数，可能是同步，也可能是异步, 这里我们就来写一个异步的执行
    //     setTimeout(() => {
    //         resolve('hello');
    //     })
    // })

    // promise.then(data => {
    //     console.log(data);
    // }, err => {
    //     console.log(err)
    // })]
    class _Promise {
        constructor(exector) {
            let self = this;
            this.status = "pending";
            this.value;
            this.reason;
            this.onResolvedCallbacks = [];
            this.onRejectedCallbacks = [];

            function success(value) {
                if (self.status === "pending") {
                    self.value = value;
                }
                self.status = "resolved";
                self.onResolvedCallbacks.forEach((fn) => {
                    fn();
                });
            }

            function error(reason) {
                if (self.status === "pending") {
                    self.reason = reason;
                }
                self.status = 'rejected';
                self.onRejectedCallbacks.forEach((fn) => {
                    fn();
                });
            }

            try {
                exector(success, error);
            } catch (e) {
                error(e);
            }
        }
        // then(onResolved, onRejected) {
        //     let self = this;
        //     if (this.status === "resolved") {
        //         onResolved(self.value);
        //     } else if (this.status === "rejected") {
        //         onRejected(self.reason);
        //     } else if (this.status === 'pending') {
        //         this.onResolvedCallbacks.push(() => {
        //             onResolved(self.value);
        //         })
        //         this.onRejectedCallbacks.push(() => {
        //             onRejected(self.reason)
        //         });
        //     }

        // }
        then(onFulfilled, onRejected) {

            let self = this;

            function resolvePromise(promise2, x, resolve, reject) {
                if (promise2 === x) {
                    return reject(new TypeError('Chaining cycle'));
                }
                if (x !== null && (typeof x === 'object' || typeof x === 'function')) {
                    try {
                        let then = x.then;
                        if (typeof then === 'function') {
                            then.call(x, y => {
                                resolvePromise(promise2, y, resolve, reject);
                            }, err => {
                                reject(err);
                            });
                        } else {
                            resolve(x);
                        }
                    } catch (e) {
                        reject(e);
                    }
                } else {
                    resolve(x);
                }
            }
            let promise2 = new _Promise((resolve, reject) => {
                if (this.status === 'resolved') {
                    try {
                        let x = onFulfilled(self.value);
                        resolvePromise(promise2, x, resolve, reject);
                    } catch (e) {
                        reject(e);
                    }
                }

                if (this.status === 'rejected') {
                    try {
                        let x = onRejected(self.reason);
                        resolvePromise(promise2, x, resolve, reject);
                    } catch (e) {
                        reject(e);
                    }
                }
                if (this.status === 'pending') {
                    this.onResolvedCallbacks.push(() => {
                        try {
                            let x = onFulfilled(self.value);
                            resolvePromise(promise2, x, resolve, reject);
                        } catch (e) {
                            reject(e);
                        }

                    })
                    this.onRejectedCallbacks.push(() => {
                        try {
                            let x = onRejected(self.reason);
                            resolvePromise(promise2, x, resolve, reject);
                        } catch (e) {
                            reject(e);
                        }
                    });
                }
            })
            return promise2;
        }

    }
    let p = new _Promise((resolve, reject) => {
        setTimeout(() => {
            resolve('hello');
        })
    })

    let p2 = p.then(data => {
        return p2;
    })



    // let promise = new _Promise((resolve, reject) => {
    //     if (Math.random() > 0) {
    //         resolve('成功');
    //     } else {
    //         reject('失败');
    //     }
    // })
    // // for (var i = 0; i < 1000; i++) {
    // //     console.log(1)
    // // }
    // console.log(promise.then(data => {
    //     console.log("sudo");
    // }))

    // url1 = "http://127.0.0.1/myown/promise/php/data1.php"
    // url2 = "http://127.0.0.1/myown/promise/php/data2.php"
    // url3 = "http://127.0.0.1/myown/promise/php/data3.php"

    // function getAjax(url, data) {
    //     var p = new _Promise(function (success, error) {
    //         var str = "";
    //         data = data || {};
    //         var xhr = new XMLHttpRequest();
    //         for (var i in data) {
    //             str += `${i}=${data[i]}&`;
    //         }
    //         str = str.slice(0, str.length - 1);
    //         url = url + "?" + str + "__retr0__=" + new Date().getDate();
    //         xhr.open("get", url, true);
    //         xhr.onreadystatechange = function () {
    //             if (xhr.readyState === 4 && xhr.status === 200) {
    //                 success(xhr.responseText);
    //             } else if (xhr.readyState === 4 && xhr.status != 200) {
    //                 error(xhr.status);
    //             }
    //         }
    //         xhr.send();
    //     })
    //     return p;
    // }
    // var p1 = getAjax(url1).then(function (res) {
    //     console.log(res);
    // }, function (res) {
    //     console.log(res)
    // })
    // var p2 = getAjax(url2).then(function (res) {
    //     console.log("jQuery");
    // }, function (res) {
    //     console.log(res)
    // })
    // var p3 = getAjax(url3).then(function (res) {
    //     console.log("jQuery");
    // }, function (res) {
    //     console.log(res)
    // })
    // Promise.all([p1, p2, p3])
```

</details>

<hr>

### **2020/01/06**⌚️

- 结果是什么?

    ```js
    Promise.resolve(5)
    ```

    

    <details >
          <summary>点击</summary>

    我们可以将我们想要的任何类型的值传递`Promise.resolve`，无论是否`promise`。 该方法本身返回带有已解析值的`Promise`。 如果您传递常规函数，它将是具有常规值的已解决`promise`。 如果你通过了promise，它将是一个已经resolved的且带有传的值的promise。

    上述情况，我们传了数字5，因此返回一个resolved状态的promise，resolve值为`5`
      </details>

<hr>

### **2020/01/07**⌚️

- 哪些方法修改了原数组?

  ```js
  const emojis = ['✨', '🥑', '😍']
  
  emojis.map(x => x + '✨')
  emojis.filter(x => x !== '🥑')
  emojis.find(x => x !== '🥑')
  emojis.reduce((acc, cur) => acc + '✨')
  emojis.slice(1, 2, '✨') 
  emojis.splice(1, 2, '✨')
  ```

  

  <details >
        <summary>点击</summary>
        <ul>
            <li>使用`splice`方法，我们通过删除，替换或添加元素来修改原始数组。 在这种情况下，我们从索引1中删除了2个元素（我们删除了`'🥑'`和`'😍'`），同时添加了![sparkles](https://github.githubassets.com/images/icons/emoji/unicode/2728.png)emoji表情。</li>
            <li>`map`，`filter`和`slice`返回一个新数组，`find`返回一个元素，而`reduce`返回一个减小的值。</li>
        </ul>
    </details>

<hr>

### **2020/01/08**⌚️

- 输出什么?

  ```js
  const food = ['🍕', '🍫', '🥑', '🍔']
  const info = { favoriteFood: food[0] }
  
  info.favoriteFood = '🍝'
  
  console.log(food)
  ```

  <details >
        <summary>点击</summary>

  我们将`info`对象上的`favoriteFood`属性的值设置为披萨表情符号“![pizza](https://github.githubassets.com/images/icons/emoji/unicode/1f355.png)”的字符串。字符串是原始数据类型。在JavaScript中，原始数据类型通过值起作用

  在这种情况下，我们将`info`对象上的`favoriteFood`属性的值设置为等于`food`数组中的第一个元素的值，字符串为披萨表情符号（`'🍕'` ）。字符串是原始数据类型，并且通过值进行交互，我们更改`info`对象上`favoriteFood`属性的值。 food数组没有改变，因为favoriteFood的值只是该数组中第一个元素的值的复制，并且与该元素上的元素没有相同的内存引用食物`[0]`。当我们记录食物时，它仍然是原始数组`['🍕'，'🍫'，'🥑'，'🍔']`。
    </details>

<hr>

### **2020/01/09**⌚️

- 依次输出什么

  ```js
  const myPromise = () => Promise.resolve('I have resolved!')
  
  function firstFunction() {
    myPromise().then(res => console.log(res))
    console.log('second')
  }
  
  async function secondFunction() {
    console.log(await myPromise())
    console.log('second')
  }
  
  firstFunction()
  secondFunction()
  ```

  

  <details >
        <summary>点击</summary>

  <li>`second`, `I have resolved!` and `I have resolved!`, `second`</li>

  <li> 有了promise，我们通常会说：当我想要调用某个方法，但是由于它可能需要一段时间，因此暂时将它放在一边。只有当某个值被resolved/rejected，并且执行栈为空时才使用这个值。

  我们可以在`async`函数中通过`.then`和`await`关键字获得该值。 尽管我们可以通过`.then`和`await`获得promise的价值，但是它们的工作方式有所不同。

  在 `firstFunction`中，当运行到`myPromise`方法时我们将其放在一边，即promise进入微任务队列，其他后面的代码（`console.log('second')`）照常运行，因此`second`被打印出，`firstFunction`方法到此执行完毕，执行栈中宏任务队列被清空，此时开始执行微任务队列中的任务，`I have resolved`被打印出。

  在`secondFunction`方法中，我们通过`await`关键字，暂停了后面代码的执行，直到异步函数的值被解析才开始后面代码的执行。这意味着，它会等着直到 `myPromise` 以值`I have resolved`被解决之后，下一行`second`才开始执行。</li>

    </details>

<hr>

### **2020/01/10**⌚️

- 输出是什么？

  ```js
  [[0, 1], [2, 3]].reduce(
    (acc, cur) => {
      return acc.concat(cur)
    },
    [1, 2]
  )
  ```

  

  <details >
        <summary>点击</summary>

  `[1, 2]`是初始值。初始值将会作为首次调用时第一个参数 `acc` 的值。在第一次执行时， `acc` 的值是 `[1, 2]`， `cur` 的值是 `[0, 1]`。合并它们，结果为 `[1, 2, 0, 1]`。 第二次执行， `acc` 的值是 `[1, 2, 0, 1]`， `cur` 的值是 `[2, 3]`。合并它们，最终结果为 `[1, 2, 0, 1, 2, 3]`
    </details>

<hr>

### **2020/01/11**⌚️

- $().load怎么使用

  <details >
        <summary>点击</summary>

  - HTML

    ```html
    <div class="top">
        <h1>子页</h1>
    </div>
    <div class="box"></div>
    <div class="footer"></div>
    ```

  - JS

    用法是在load()方法中传入绝对坐标的URL地址字符，地址后`空格加CSS选择器字符`可以实现选择具体的元素插入

    ```js
    $(".box").load("http://localhost/1912-server/jq-ajax/data/page.html .nav");
    $(".footer").load("http://localhost/1912-server/jq-ajax/data/page.html p");
    ```

  - 外部HTML

    ```html
    <div class="nav">导航</div>
    <p>页脚</p>
    ```

      </details>

<hr>

### **2020/01/12**⌚️

- 用$.ajax()如何实现loading效果

  <details >
        <summary>点击</summary>

  ```js
  $("document").on("click",()=>{
      var xhr = $.ajax({
          url: "http://127.0.0.1/myown/jq-ajax/data/loading.php",
          success:function(res){
              console.log(res);
              $("img").hide();
          },
          beforesend:function(){
                  if($("img")[0]){
                      $("body").append($("<img src = '1.jpg' class='loading'>"));
                  }else{
  	 				$("img").show();
                  }
              }
          }
      })
  })
  ```

  

    </details>

<hr>

### **2020/01/13**⌚️

-  输出是什么？

  ```js
  [...'Lydia']
  ```

  - A: `["L", "y", "d", "i", "a"]`
  - B: `["Lydia"]`
  - C: `[[], "Lydia"]`
  - D: `[["L", "y", "d", "i", "a"]]`

  

  <details >
        <summary>点击</summary>

  A:	string 类型是可迭代的。扩展运算符将迭代的每个字符映射成一个元素。
    </details>

<hr>

### **2020/01/14**⌚️

- 输出是什么？

  ```js
  ['1','7','11'].map(parseInt)
  ```

  <details >
        <summary>点击</summary>

  <ul>

  <li>首先,arr.map()方法中的回调函数接受3个参数,分别为ele,val,self,即每个值,索引,数组自身</li>

  <li>其次,parseInt函数接受2个参数,分为是val,num,即需要转成数值的字符和按照几进制转换</li>

  <li>map第一次遍历,传给parseInt(1,0),得到1,因为第二个参数为0,默认按10进制</li>

  <li>map第二次遍历,传给parseInt(7,1),得到NAN,因为第二个参数为1,默认按1进制,报错</li>

  <li>map第三次遍历,传给parseInt(11,2),得到3,因为第二个参数为2,默认按2进制</li>

  </ul>
    </details>

<hr>

### **2020/01/15**⌚️

- 输出是什么？

  ```js
  const numbers = [1, 2, 3, 4, 5];
  const [y] = numbers;
  
  console.log(y);
  ```

  - A: `[[1, 2, 3, 4, 5]]`
  - B: `[1, 2, 3, 4, 5]`
  - C: `1`
  - D: `[1]`

  <details >
        <summary>点击</summary>

  #### 答案: C

  我们可以通过解构赋值来解析来自对象的数组或属性的值，比如说：

  ```
  [a, b] = [1, 2];
  ```

  ![img](https://camo.githubusercontent.com/8903a861b474f8b63da9d0d46d14a74d9e2db039/68747470733a2f2f692e696d6775722e636f6d2f41444670566f702e706e67)

  `a`的值现在是`1`，`b`的值现在是`2`.而在题目中，我们是这么做的:

  ```
  [y] = [1, 2, 3, 4, 5];
  ```

  ![img](https://camo.githubusercontent.com/3474488027d64c5fc9955ab5be7c3a88d1254449/68747470733a2f2f692e696d6775722e636f6d2f4e7a476b4d4e6b2e706e67)

  也就是说，`y`等于数组的第一个值就是数字`1`.我们输出`y`， 返回`1`.
    </details>

<hr>

### **2020/01/16**⌚️

- 输出是什么？

  ```js
  const obj = { a: 'one', b: 'two', a: 'three' }
  console.log(obj)
  ```

  - A: `{ a: "one", b: "two" }`
  - B: `{ b: "two", a: "three" }`
  - C: `{ a: "three", b: "two" }`
  - D: `SyntaxError`

  <details >
        <summary>点击</summary>

  如果你有两个名称相同的键，则键会被替换掉。它仍然位于第一个键出现的位置，但是值是最后出现那个键的值。
    </details>

<hr>

### **2020/01/17**⌚️

- 输出是什么？

  ```js
  const person = {
    name: "Lydia",
    age: 21
  }
  
  for (const [x, y] of Object.entries(person)) {
    console.log(x, y)
  }
  ```

  - A: `name` `Lydia` and `age` `21`
  - B: `["name", "Lydia"]` and `["age", 21]`
  - C: `["name", "age"]` and `undefined`
  - D: `Error`

  <details >
        <summary>点击</summary>

  #### 答案: A

  `Object.entries()`方法返回一个给定对象自身可枚举属性的键值对数组，上述情况返回一个二维数组，数组每个元素是一个包含键和值的数组：

  `[['name'，'Lydia']，['age'，21]]`

  使用`for-of`循环，我们可以迭代数组中的每个元素，上述情况是子数组。 我们可以使用`const [x，y]`在`for-of`循环中解构子数组。 `x`等于子数组中的第一个元素，`y`等于子数组中的第二个元素。

  第一个子阵列是`[“name”，“Lydia”]`，其中`x`等于`name`，而`y`等于`Lydia`。 第二个子阵列是`[“age”，21]`，其中`x`等于`age`，而`y`等于`21`。
    </details>

<hr>

### **2020/01/18**⌚️

- 输出是什么？

  ```js
  const set = new Set()
  
  set.add(1)
  set.add("Lydia")
  set.add({ name: "Lydia" })
  
  for (let item of set) {
    console.log(item + 2)
  }
  ```

  - A: `3`, `NaN`, `NaN`
  - B: `3`, `7`, `NaN`
  - C: `3`, `Lydia2`, `[Object object]2`
  - D: `"12"`, `Lydia2`, `[Object object]2`

  <details >
        <summary>点击</summary>

  “+”运算符不仅用于添加数值，还可以使用它来连接字符串。 每当JavaScript引擎发现一个或多个值不是数字时，就会将数字强制为字符串。

  第一个是数字1。 1 + 2返回数字3。

  但是，第二个是字符串“Lydia”。 “Lydia”是一个字符串，2是一个数字：2被强制转换为字符串。 “Lydia”和“2”被连接起来，产生字符串“Lydia2”。

  `{name：“ Lydia”}`是一个对象。 数字和对象都不是字符串，因此将二者都字符串化。 每当我们对常规对象进行字符串化时，它就会变成`[Object object]`。 与“2”串联的“ [Object object]”成为“[Object object]2” 。
    </details>

<hr>

### **2020/01/19**⌚️

- 输出是什么？

  ```js
  const box = { x: 10, y: 20 };
  
  Object.freeze(box);
  
  const shape = box;
  shape.x = 100;
  console.log(shape)
  ```

  - A: `{ x: 100, y: 20 }`
  - B: `{ x: 10, y: 20 }`
  - C: `{ x: 100 }`
  - D: `ReferenceError`

  <details >
        <summary>点击</summary>

  `Object.freeze`使得无法添加、删除或修改对象的属性（除非属性的值是另一个对象）。

  当我们创建变量`shape`并将其设置为等于冻结对象`box`时，`shape`指向的也是冻结对象。你可以使用`Object.isFrozen`检查一个对象是否被冻结，上述情况，`Object.isFrozen（shape）`将返回`true`。

  由于`shape`被冻结，并且`x`的值不是对象，所以我们不能修改属性`x`。 `x`仍然等于`10`，`{x：10，y：20}`被打印。

  注意，上述例子我们对属性`x`进行修改，可能会导致抛出TypeError异常（最常见但不仅限于严格模式下时）。
    </details>

<hr>

### **2020/01/20**⌚️

- 输出是什么？

  ```js
  function nums(a, b) {
    if
    (a > b)
    console.log('a is bigger')
    else 
    console.log('b is bigger')
    return 
    a + b
  }
  
  console.log(nums(4, 2))
  console.log(nums(1, 2))
  ```

  - A: `a is bigger`, `6` and `b is bigger`, `3`
  - B: `a is bigger`, `undefined` and `b is bigger`, `undefined`
  - C: `undefined` and `undefined`
  - D: `SyntaxError`

  <details >
        <summary>点击</summary>

  在JavaScript中，我们不必显式地编写分号(`;`)，但是JavaScript引擎仍然在语句之后自动添加分号。这称为**自动分号插入**。例如，一个语句可以是变量，或者像`throw`、`return`、`break`这样的关键字。

  在这里，我们在新的一行上写了一个`return`语句和另一个值`a + b `。然而，由于它是一个新行，引擎并不知道它实际上是我们想要返回的值。相反，它会在`return`后面自动添加分号。你可以这样看:

  ```
    return;
    a + b
  ```

  这意味着永远不会到达`a + b`，因为函数在`return`关键字之后停止运行。如果没有返回值，就像这里，函数返回`undefined`。注意，在`if/else`语句之后没有自动插入!
    </details>

<hr>

### **2020/01/21**⌚️

- 输出是什么？

  ```js
  const name = "Lydia"
  
  console.log(name())
  ```

  - A: `SyntaxError`
  - B: `ReferenceError`
  - C: `TypeError`
  - D: `undefined`

  <details >
        <summary>点击</summary>

  变量`name`保存字符串的值，该字符串不是函数，因此无法调用。

  当值不是预期类型时，会抛出`TypeErrors`。 JavaScript期望`name`是一个函数，因为我们试图调用它。 但它是一个字符串，因此抛出`TypeError`：`name is not a function`

  当你编写了一些非有效的JavaScript时，会抛出语法错误，例如当你把`return`这个词写成`retrun`时。 当JavaScript无法找到您尝试访问的值的引用时，抛出`ReferenceErrors`。
    </details>

<hr>

### **2020/01/22**⌚️

- 输出是什么？

  ```js
  const set = new Set()
  
  set.add(1)
  set.add("Lydia")
  set.add({ name: "Lydia" })
  
  for (let item of set) {
    console.log(item + 2)
  }
  ```

  - A: `3`, `NaN`, `NaN`
  - B: `3`, `7`, `NaN`
  - C: `3`, `Lydia2`, `[Object object]2`
  - D: `"12"`, `Lydia2`, `[Object object]2`

  <details >
        <summary>点击</summary>

  “+”运算符不仅用于添加数值，还可以使用它来连接字符串。 每当JavaScript引擎发现一个或多个值不是数字时，就会将数字强制为字符串。

  第一个是数字1。 1 + 2返回数字3。

  但是，第二个是字符串“Lydia”。 “Lydia”是一个字符串，2是一个数字：2被强制转换为字符串。 “Lydia”和“2”被连接起来，产生字符串“Lydia2”。

  `{name：“ Lydia”}`是一个对象。 数字和对象都不是字符串，因此将二者都字符串化。 每当我们对常规对象进行字符串化时，它就会变成`[Object object]`。 与“2”串联的“ [Object object]”成为“[Object object]2”。
    </details>

<hr>

### **2020/01/23**⌚️

- 输出是什么？

  ```js
  JSON.parse()
  ```

  - A: Parses JSON to a JavaScript value
  - B: Parses a JavaScript object to JSON
  - C: Parses any JavaScript value to JSON
  - D: Parses JSON to a JavaScript object only

  <details >
        <summary>点击</summary>

  #### 答案: A

  使用`JSON.parse()`方法，我们可以将JSON字符串解析为JavaScript值。

  ```
  // 将数字字符串化为有效的JSON，然后将JSON字符串解析为JavaScript值:
  const jsonNumber = JSON.stringify(4) // '4'
  JSON.parse(jsonNumber) // 4
  
  // 将数组值字符串化为有效的JSON，然后将JSON字符串解析为JavaScript值:
  const jsonArray = JSON.stringify([1, 2, 3]) // '[1, 2, 3]'
  JSON.parse(jsonArray) // [1, 2, 3]
  
  // 将对象字符串化为有效的JSON，然后将JSON字符串解析为JavaScript值:
  const jsonArray = JSON.stringify({ name: "Lydia" }) // '{"name":"Lydia"}'
  JSON.parse(jsonArray) // { name: 'Lydia' }
  ```

    </details>

<hr>

### **2020/01/24**⌚️

- 输出是什么？

  ```js
  const one = (false || {} || null)
  const two = (null || false || "")
  const three = ([] || 0 || true)
  
  console.log(one, two, three)
  ```

  - A: `false` `null` `[]`
  - B: `null` `""` `true`
  - C: `{}` `""` `[]`
  - D: `null` `null` `true`

  <details >
        <summary>点击</summary>

  #### 答案: C

  使用`||`运算符，我们可以返回第一个真值。 如果所有值都是假值，则返回最后一个值。

  `（false || {} || null）`：空对象`{}`是一个真值。 这是第一个（也是唯一的）真值，它将被返回。`one`等于`{}`。

  `（null || false ||“”）`：所有值都是假值。 这意味着返回传递的值`""`。 `two`等于`""`。

  `（[] || 0 ||“”）`：空数组`[]`是一个真值。 这是第一个返回的真值。 `three`等于`[]`。

   </details>

<hr>

### **2020/01/25**⌚️

- 输出是什么？

  ```js
  console.log(`${(x => x)('I love')} to program`)
  ```

  - A: `I love to program`
  - B: `undefined to program`
  - C: `${(x => x)('I love') to program`
  - D: `TypeError`

  <details >
        <summary>点击</summary>

  #### 答案: A

  带有模板字面量的表达式首先被执行。相当于字符串会包含表达式，这个立即执行函数 `(x => x)('I love')` 返回的值. 我们向箭头函数 `x => x` 传递 `'I love'` 作为参数。`x` 等价于返回的 `'I love'`。这就是结果 `I love to program`。

   </details>

<hr>

### **2020/01/26**⌚️

- 将会发生什么?

  ```js
  let config = {
    alert: setInterval(() => {
      console.log('Alert!')
    }, 1000)
  }
  
  config = null
  ```

  - A: `setInterval` 的回调不会被调用
  - B: `setInterval` 的回调被调用一次
  - C: `setInterval` 的回调仍然会被每秒钟调用
  - D: 我们从没调用过 `config.alert()`, config 为 `null`

  <details >
        <summary>点击</summary>


  #### 答案: A

  一般情况下当我们将对象赋值为 `null`, 那些对象会被进行 *垃圾回收（garbage collected）* 因为已经没有对这些对象的引用了。然而，`setInterval`的参数是一个箭头函数（所以上下文绑定到对象 `config` 了），回调函数仍然保留着对 `config`的引用。只要存在引用，对象就不会被垃圾回收。因为没有被垃圾回收，`setInterval` 的回调每1000ms (1s)会被调用一次。

   </details>

<hr>

### **2020/01/27**⌚️

- 会输出什么?

  ```js
  const config = {
  	languages: [],
  	set language(lang) {
  		return this.languages.push(lang);
  	}
  };
  
  console.log(config.language);
  ```

  - A: `function language(lang) { this.languages.push(lang }`
  - B: `0`
  - C: `[]`
  - D: `undefined`

  <details >
        <summary>点击</summary>

  #### 答案: A

  方法 `language` 是一个 `setter`。Setters 并不保存一个实际值，它们的使命在于 *修改* 属性。当调用方法 `setter`， 返回 `undefined`。


  #### 一、什么是getter和setter

  - getter 是一种获得属性值的方法，setter是一种设置属性值的方法
  - getter负责查询值，它不带任何参数，setter则负责设置键值，值是以参数的形式传递，在他的函数体中，一切的return都是无效的
  - get/set访问器不是对象的属性，而是属性的特性，特性只有内部才用，因此在javaScript中不能直接访问他们，为了表示特性是内部值用两队中括号括起来表示如[[Value]]
  - 对象的属性又可分为对象属性和访问器属性（参考资料： [https://www.cnblogs.com/absolute-child/p/7188417.html](https://www.cnblogs.com/lvmylife/p/%20https://www.cnblogs.com/absolute-child/p/7188417.html)）

  #### 二、使用方式

  ##### 2.1 set/get


  ```
  var person = {
      _name: '',
      get name() { return this._name },
      set name(n) { this._name = n }
  }
   
  // 测试
  person.name // 输出 --> ''
  person.name = 'Zhangsan'
  person.name // 输出 --> Zhangsan
  ```


  ##### 2.2 Object.defineProperty


  ```
  var person = function() {
      var _name = ' ';
      var obj = {};
      Object.defineProperty(obj, 'name', {
          configurable: true,
          enumerable: true,
          get: function() {
              return _name;
          },
          set: function(n) {
              _name = n;
          }
      })
      return obj;
  }();
  person.name = "Zhangsan";
  person.name // 输出 --> Zhangsan
  ```
</details>

<hr>

### **2020/01/28**⌚️

- 输出是什么？

  ```js
  const person = {
  	name: "Lydia Hallie",
  	hobbies: ["coding"]
  };
  
  function addHobby(hobby, hobbies = person.hobbies) {
  	hobbies.push(hobby);
  	return hobbies;
  }
  
  addHobby("running", []);
  addHobby("dancing");
  addHobby("baking", person.hobbies);
  
  console.log(person.hobbies);
  ```

  - A: `["coding"]`
  - B: `["coding", "dancing"]`
  - C: `["coding", "dancing", "baking"]`
  - D: `["coding", "running", "dancing", "baking"]`

  <details >
        <summary>点击</summary>

  #### 答案: C

  函数 `addHobby` 接受两个参数，`hobby` 和有着对象 `person` 中数组 `hobbies` 默认值的 `hobbies`。

  首先，我们调用函数 `addHobby`，并给 `hobby` 传递 `"running"` 以及给 `hobbies` 传递一个空数组。因为我们给 `hobbies` 传递了空数组，`"running"` 被添加到这个空数组。

  然后，我们调用函数 `addHobby`，并给 `hobby` 传递 `"dancing"`。我们不向 `hobbies` 传递值，因此它获取其默认值 —— 对象 `person` 的 属性 `hobbies`。我们向数组 `person.hobbies` push `dancing`。

  最后，我们调用函数 `addHobby`，并向 `hobby` 传递 值 `"bdaking"`，并且向 `hobbies` 传递 `person.hobbies`。我们向数组 `person.hobbies` push `dancing`。

  pushing `dancing` 和 `baking` 之后，`person.hobbies` 的值为 `["coding", "dancing", "baking"]`

   </details>

<hr>

### **2020/01/29**⌚️

- 返回值是什么?

  ```js
  const firstPromise = new Promise((res, rej) => {
    setTimeout(res, 500, "one");
  });
  
  const secondPromise = new Promise((res, rej) => {
    setTimeout(res, 100, "two");
  });
  
  Promise.race([firstPromise, secondPromise]).then(res => console.log(res));
  ```

  - A: `"one"`
  - B: `"two"`
  - C: `"two" "one"`
  - D: `"one" "two"`

  <details >
        <summary>点击</summary>

  #### 答案: B

  当我们向`Promise.race`方法中传入多个`Promise`时，会进行 *优先* 解析。在这个例子中，我们用`setTimeout`给`firstPromise`和`secondPromise`分别设定了500ms和100ms的定时器。这意味着`secondPromise`会首先解析出字符串`two`。那么此时`res`参数即为`two`，是为输出结果。

   </details>

<hr>

### **2020/01/30**⌚️

- 输出什么？

  ```js
  function* generatorOne() {
    yield ['a', 'b', 'c'];
  }
  
  function* generatorTwo() {
    yield* ['a', 'b', 'c'];
  }
  
  const one = generatorOne()
  const two = generatorTwo()
  
  console.log(one.next().value)
  console.log(two.next().value)
  ```

  - A: `a` and `a`
  - B: `a` and `undefined`
  - C: `['a', 'b', 'c']` and `a`
  - D: `a` and `['a', 'b', 'c']`

  <details >
        <summary>点击</summary>

  #### 答案: C

  通过 `yield` 关键字, 我们在 `Generator` 函数里执行`yield`表达式. 通过 `yield*` 关键字, 我们可以在一个`Generator` 函数里面执行（`yield`表达式）另一个 `Generator` 函数, 或可遍历的对象 (如数组).

  在函数 `generatorOne` 中, 我们通过 `yield` 关键字 yield 了一个完整的数组 `['a', 'b', 'c']`。函数`one`通过`next`方法返回的对象的`value` 属性的值 (`one.next().value`) 等价于数组 `['a', 'b', 'c']`.

  ```
  console.log(one.next().value) // ['a', 'b', 'c']
  console.log(one.next().value) // undefined
  ```

  在函数 `generatorTwo` 中, 我们使用 `yield*` 关键字。就相当于函数`two`第一个`yield`的值, 等价于在迭代器中第一个 `yield` 的值。数组`['a', 'b', 'c']`就是这个迭代器. 第一个 `yield` 的值就是 `a`, 所以我们第一次调用 `two.next().value`时, 就返回`a`。

  ```
  console.log(two.next().value) // 'a'
  console.log(two.next().value) // 'b'
  console.log(two.next().value) // 'c'
  console.log(two.next().value) // undefined
  ```

   </details>

<hr>

### **2020/01/31**⌚️

- 输出什么？

  ```js
  const colorConfig = {
    red: true,
    blue: false,
    green: true,
    black: true,
    yellow: false,
  }
  
  const colors = ["pink", "red", "blue"]
  
  console.log(colorConfig.colors[1])
  ```

  - A: `true`
  - B: `false`
  - C: `undefined`
  - D: `TypeError`

  <details >
        <summary>点击</summary>答案: D

  在JavaScript中，我们有两种访问对象属性的方法：括号表示法或点表示法。 在此示例中，我们使用点表示法（`colorConfig.colors`）代替括号表示法（`colorConfig [“ colors”]`）。

  使用点表示法，JavaScript会尝试使用该确切名称在对象上查找属性。 在此示例中，JavaScript尝试在colorconfig对象上找到名为colors的属性。 没有名为“colors”的属性，因此返回“undefined”。 然后，我们尝试使用`[1]`访问第一个元素的值。 我们无法对未定义的值执行此操作，因此会抛出`Cannot read property '1' of undefined`。

  JavaScript解释（或取消装箱）语句。 当我们使用方括号表示法时，它会看到第一个左方括号`[`并一直进行下去，直到找到右方括号`]`。 只有这样，它才会评估该语句。 如果我们使用了colorConfig [colors [1]]，它将返回colorConfig对象上red属性的值。

   </details>

<hr>

### **2020/02/01**⌚️

- 输出什么？

  ```js
  const myFunc = ({ x, y, z }) => {
  	console.log(x, y, z);
  };
  
  myFunc(1, 2, 3);
  ```

  - A: `1` `2` `3`
  - B: `{1: 1}` `{2: 2}` `{3: 3}`
  - C: `{ 1: undefined }` `undefined` `undefined`
  - D: `undefined` `undefined` `undefined`

  <details >
        <summary>点击</summary>
  答案: D

  `myFunc` 期望接收一个包含 `x`, `y` 和 `z` 属性的对象作为它的参数。因为我们仅仅传递三个单独的数字值 (1, 2, 3) 而不是一个含有 `x`, `y` 和 `z` 属性的对象 ({x: 1, y: 2, z: 3})， `x`, `y` 和 `z` 有着各自的默认值 `undefined`.

  

   </details>

<hr>

### **2020/02/02**⌚️

- 输出什么？

  ```js
  const name = "Lydia Hallie";
  const age = 21;
  
  console.log(Number.isNaN(name));
  console.log(Number.isNaN(age));
  
  console.log(isNaN(name));
  console.log(isNaN(age));
  ```

  - A: `true` `false` `true` `false`
  - B: `true` `false` `false` `false`
  - C: `false` `false` `true` `false`
  - D: `false` `true` `false` `true`

  <details >
        <summary>点击</summary>
  答案: C

  通过方法 `Number.isNaN`，你可以检测你传递的值是否为 *数字值* 并且是否等价于 `NaN`。`name` 不是一个数字值，因此 `Number.isNaN(name)` 返回 `false`。`age` 是一个数字值，但它不等价于 `NaN`，因此 `Number.isNaN(age)` 返回 `false`.

  通过方法 `isNaN`， 你可以检测你传递的值是否一个 number。`name` 不是一个 `number`，因此 `isNaN(name)` 返回 `true`. `age` 是一个 `number` 因此 `isNaN(age)` 返回 `false`.

  ### 令人费解的怪异行为

  如果`isNaN`函数的参数不是`Number`类型， `isNaN`函数会首先尝试将这个参数转换为数值，然后才会对转换后的结果是否是[`NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN)进行判断。因此，对于能被强制转换为有效的非NaN数值来说（空字符串和布尔值分别会被强制转换为数值0和1），返回`false`值也许会让人感觉莫名其妙。比如说，空字符串就明显“不是数值（not a number）”。这种怪异行为起源于："不是数值（not a number）"在基于IEEE-754数值的浮点计算体制中代表了一种特定的含义。`isNaN`函数其实等同于回答了这样一个问题：被测试的值在被强制转换成数值时会不会返回IEEE-754中所谓的“不是数值（not a number）”。

  

   </details>

<hr>

### **2020/02/03**⌚️

- 输出什么？

  ```js
  const add = () => {
    const cache = {};
    return num => {
      if (num in cache) {
        return `From cache! ${cache[num]}`;
      } else {
        const result = num + 10;
        cache[num] = result;
        return `Calculated! ${result}`;
      }
    };
  };
  
  const addFunction = add();
  console.log(addFunction(10));
  console.log(addFunction(10));
  console.log(addFunction(5 * 2));
  ```

  - A: `Calculated! 20` `Calculated! 20` `Calculated! 20`
  - B: `Calculated! 20` `From cache! 20` `Calculated! 20`
  - C: `Calculated! 20` `From cache! 20` `From cache! 20`
  - D: `Calculated! 20` `From cache! 20` `Error`

  <details >
        <summary>点击</summary>
  答案: C
`add`函数是一个记忆函数。 通过记忆化，我们可以缓存函数的结果，以加快其执行速度。上述情况，我们创建一个`cache`对象，用于存储先前返回过的值。
  
  

如果我们使用相同的参数多次调用`addFunction`函数，它首先检查缓存中是否已有该值，如果有，则返回缓存值，这将节省执行时间。如果没有，那么它将计算该值，并存储在缓存中。

我们用相同的值三次调用了`addFunction`函数：

在第一次调用，`num`等于`10`时函数的值尚未缓存，if语句`num in cache`返回`false`，else块的代码被执行：`Calculated! 20`，并且其结果被添加到缓存对象，`cache`现在看起来像`{10：20}`。

第二次，`cache`对象包含`10`的返回值。 if语句 `num in cache` 返回`true`，`From cache! 20`被打印。

第三次，我们将`5 * 2`(值为10)传递给函数。 `cache`对象包含`10`的返回值。 if语句 `num in cache` 返回`true`，`From cache! 20`被打印。



 </details>

<hr>

### **2020/02/04**⌚️

- 输出什么？

  ```js
  const add = x => y => z => {
  	console.log(x, y, z);
  	return x + y + z;
  };
  
  add(4)(5)(6);
  ```
  
  - A: `4` `5` `6`
  - B: `6` `5` `4`
  - C: `4` `function` `function`
  - D: `undefined` `undefined` `6`
  
  <details >
        <summary>点击</summary>
        答案: A

  
  函数 `add` 是一个返回 返回箭头函数的箭头函数 的箭头函数（still with me?）。第一个函数接收一个值为 `4` 的参数 `x`。我们调用第二个函数，它接收一个值为 `5` 的参数 `y`。然后我们调用第三个函数，它接收一个值为 `6` 的参数 `z`。当我们尝试在最后一个箭头函数中获取 `x`, `y` 和 `z` 的值，JS 引擎根据作用域链去找 `x` 和 `y` 的值。得到 `4` `5` `6`.

 </details>

<hr>

### **2020/02/05**⌚️

- 输出什么？

  ```js
  class Person {
    constructor(name) {
      this.name = name
    }
  }
  
  const member = new Person("John")
  console.log(typeof member)
  ```

  - A: `"class"`
  - B: `"function"`
  - C: `"object"`
  - D: `"string"`

  <details >
        <summary>点击</summary>
        答案: C

  

  类是构造函数的语法糖，如果用构造函数的方式来重写`Person`类则将是：

  ```
  function Person() {
    this.name = name
  }
  ```

  通过`new`来调用构造函数，将会生成构造函数`Person`的实例，对实例执行`typeof`关键字将返回`"object"`，上述情况打印出`"object"`。

 </details>

<hr>

### **2020/02/06**⌚️

- 输出什么？

  ```js
  let name = 'Lydia'
  
  function getName() {
    console.log(name)
    let name = 'Sarah'
  }
  
  getName()
  ```

  - A: Lydia
  - B: Sarah
  - C: `undefined`
  - D: `ReferenceError`

  <details >
        <summary>点击</summary>
        答案: D

  

  每个函数都有其自己的执行上下文。 `getName`函数首先在其自身的上下文（范围）内查找，以查看其是否包含我们尝试访问的变量`name`。 上述情况，`getName`函数包含其自己的`name`变量：我们用`let`关键字和`Sarah`的值声明变量`name`。

  带有`let`关键字（和`const`）的变量被提升，但是与`var`不同，它不会被***初始化***。 在我们声明（初始化）它们之前，无法访问它们。 这称为“暂时性死区”。 当我们尝试在声明变量之前访问变量时，JavaScript会抛出`ReferenceError: Cannot access 'name' before initialization`。
  
  如果我们不在`getName`函数中声明`name`变量，则javascript引擎会查看原型练。会找到其外部作用域有一个名为`name`的变量，其值为`Lydia`。 在这种情况下，它将打印`Lydia`：
  
  ```
let name = 'Lydia'
  
  function getName() {
    console.log(name)
  }
  
  getName() // Lydia
  ```

 </details>

<hr>

### **2020/02/07**⌚️

- 输出什么？

  ```js
  const settings = {
    username: "lydiahallie",
    level: 19,
    health: 90
  };
  
  const data = JSON.stringify(settings, ["level", "health"]);
  console.log(data);
  ```

  - A: `"{"level":19, "health":90}"`
  - B: `"{"username": "lydiahallie"}"`
  - C: `"["level", "health"]"`
  - D: `"{"username": "lydiahallie", "level":19, "health":90}"`

  <details >
        <summary>点击</summary>
        答案: A

  

  `JSON.stringify`的第二个参数是 *替代者(replacer)*. 替代者(replacer)可以是个函数或数组，用以控制哪些值如何被转换为字符串。

  如果替代者(replacer)是个 *数组* ，那么就只有包含在数组中的属性将会被转化为字符串。在本例中，只有名为`"level"` 和 `"health"` 的属性被包括进来， `"username"`则被排除在外。 `data` 就等于 `"{"level":19, "health":90}"`.

  而如果替代者(replacer)是个 *函数*，这个函数将被对象的每个属性都调用一遍。 函数返回的值会成为这个属性的值，最终体现在转化后的JSON字符串中（译者注：Chrome下，经过实验，如果所有属性均返回同一个值的时候有异常，会直接将返回值作为结果输出而不会输出JSON字符串），而如果返回值为`undefined`，则该属性会被排除在外。

  

 </details>

<hr>