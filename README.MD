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

### 发布-订阅的顺序探讨

我们通常所看到的都是先订阅再发布，但是必须要遵守这种顺序吗？答案是不一定的。如果发布者先发布一条消息，但是此时还没有订阅者订阅此消息，我们可以不让此消息消失于宇宙之中。就如同QQ离线消息一样，离线的消息被保存在服务器中，接收人下次登录之后，才会收到此消息。同样的，我们可以建立一个存放离线事件的堆栈，当事件发布的时候，如果此时还没有订阅者订阅这个事件，我们暂时把发布事件的动作包裹在一个函数里，这些包装函数会被存入堆栈中，等到有对象来订阅事件的时候，我们将遍历堆栈并依次执行这些包装函数，即重发里面的事件，不过离线事件的生命周期只有一次，就像qq未读消息只会提示你一次一样。

### JavaScript实现发布-订阅模式的便利性

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

### 小结

- 发布-订阅的优势很明显，做到了时间上的解耦和对象之间的解耦，从架构上看，MVC，MVVM都少不了发布-订阅的参与，我们常用的Vue也是基于发布-订阅的，最近会抽时间写下vue的源码实现，同样的node中的EventEmitter也是发布订阅的，之前也手写过它的实现。
- 发布-订阅同时也是有缺点存在的，创建订阅者本身要消耗一定的时间和内存，而且当你订阅一个消息以后，可能此消息最后都未发生，但是这个订阅者会始终存在于内存中。如果程序中大量使用发布-订阅的话，也会使得程序跟踪bug变得困难。

 

 

 

 

</details>