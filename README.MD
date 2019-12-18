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

