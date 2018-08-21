# 运行时代码求值

## 代码求值方式
1. eval() 函数
2. 函数构造器
3. 定时器
4. <script>函数


## eval 求值
> eval方法返回传入字符串最后一个表达式的执行结果，如：
  eval('3+4;5+6');  //返回 11

> eval 在调用eval方法的作用域内进行代码求值，如：

```
    var ninjia = "5";
    (function () {
        eval("var ninjia = 99");
        console.log("IIFE : "+ ninjia) ; //  IIFE : 99
    })();

    console.log(ninjia);  //5

    var tuzi = "111";
    (function () {
        eval("tuzi = -222");
        console.log("IIFE : "+ tuzi) ; //  IIFE : -222
    })();

    console.log(tuzi);  //-222
```

> 任何不是简单变量/原始值/赋值语句的内容都需要在外面包装一个括号，以便返回正确结果。

var o = eval("({ninja:1})");
var fn = eval("(function(){return 'ninja';})");

var  jsonObj = eval("("+json+")");  //转换json字符串为对象





