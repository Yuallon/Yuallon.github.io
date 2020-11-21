
- **Math.random()**：返回一个浮点型伪随机数，[0,1)

  ```
  #得到一个大于等于0，小于1之间的随机数
  function getRandom() {
    return Math.random();
  }
  
  #得到一个两数之间的随机数
  #这个例子返回了一个在指定值之间的随机数。这个值不小于 min（有可能等于），并且小于（不等于）max。
  function getRandomArbitrary(min, max) {
    return Math.random() * (max - min) + min;
  }
  
  #得到一个两数之间的随机整数
  #这个例子返回了一个在指定值之间的随机整数。这个值不小于 min （如果 min 不是整数，则不小于 min 的向上取整数），且小于（不等于）max。
  function getRandomInt(min, max) {
    min = Math.ceil(min);
    max = Math.floor(max);
    return Math.floor(Math.random() * (max - min)) + min; 
  //不含最大值，含最小值
  }
  
  #得到一个两数之间的随机整数，包括两个数在内
  #上一个例子提到的函数 getRandomInt() 结果范围包含了最小值，但不含最大值。如果你的随机结果需要同时包含最小值和最大值，怎么办呢?  getRandomIntInclusive() 函数可以实现。
  function getRandomIntInclusive(min, max) {
    min = Math.ceil(min);
    max = Math.floor(max);
    return Math.floor(Math.random() * (max - min + 1)) + min; //含最大值，含最小值 
  }
  ```

  参考：[Math.random()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math/random)

- **parseInt(string, radix)**： 解析一个字符串并返回指定基数的十进制整数， `radix` 是2-36之间的整数，表示被解析字符串的基数（即，以那种进制返回数据）。

  - `string`

    要被解析的值。如果参数不是一个字符串，则将其转换为字符串(使用  `ToString `抽象操作)。字符串开头的空白符将会被忽略。

  - `radix` 可选

    从 `2` 到 `36`，表示字符串的基数。例如指定 16 表示被解析值是十六进制数。请注意，10不是默认值！

  ```
  parseInt(4.7, 10); //返回4
  ```

  参考：[parseInt](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt)

- 

