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



### **2019/12/21**⌚️

- mysql如何取消主键的设置

<details >
<summary>点击</summary>
<ul>
<li>alter table class drop primary key;</li>
<li>alter table class modify id int(11),drop primary key;//将class表中的id 重置为普通列 </li>

</ul>
</details>

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

### **2020/01/03**⌚️

- 模块规范化的概念及优点

<details >
<summary>点击</summary>

<ul>
<li>模块规范化的概念：将项目的所有功能封装成独立的模块，模块之间按照一定的关系或者调用，实现整个项目的搭建</li>
<li>模块规范化的优点：封装，重用性强，耦合低，方便单独扩展</li>
</ul>

</details>

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