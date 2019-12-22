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





