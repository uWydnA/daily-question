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

