# Function

## 函数为第一型对象
1. 函数可以通过字面量创建
2. 函数可以赋值给变量/数组或其他对象的属性
3. 函数可以作为参数传递给函数
4. 函数可以作为返回值进行返回
5. 函数可以拥有动态创建并赋值的属性
6. 函数可以调用

## 异步事件
1. 浏览器事件，如当一个页面完成加载或卸载
2. 网络事件，如响应Ajax请求
3. 用户事件，如鼠标单击/鼠标移动等
4. 计时器事件，如超时或计时器触发

## 浏览器轮询
1. 浏览器轮询是单线程的，每个事件按照队列所放置的顺序来处理，即FIFO（先进先出）列表。
2. 每个事件都在自己的生命周期内进行处理，所有其他事件都必须等到这个事件处理结束后才能继续处理
3. 浏览器把事件放到队列上的机制是在事件轮询模型之外，确定事件何时发生并把他们放到事件队列上的过程
所处的线程，并不参与事件本身的处理


## 函数的特性
1. 所有的函数都有一个name属性，该属性保存的是该函数名称的字符串，没有名称的函数也有name属性，该属性值为空字符串
2. 命名一个函数，该名称在整个函数声明范围内有效。如果一个命名函数声明在顶层，window对象上的同名属性会引用该函数

```
(function(){

  console.log("aaa"+arguments.callee.name+
"bbb");
  console.log("---")
})()
// aaabbb
```

## 函数调用传递2个隐式参数 arguments 和 this
- arguments为类数组对象
- this 为调用上下文

## 函数调用
1. 作为函数进行调用
2. 作为方法调用，在对象上进行调用
3. 作为构造器调用，创建一个新对象
4. 利用apply或call调用

## 函数递归
1. 注意递归中引用丢失的问题

```
var ninja = {
    chirp: function(n){
        return  n>1? ninja.chirp(n-1)+"-chirp":"chirp"; //此处固定写为ninja.chirp,容易丢失！
    }
}

var samurai = {chirp:ninja.chirp};
ninja = {};
samurai.chirp(3)  ;// 错误！

```

 > 优化方案1


```
var ninja = {
    chirp: function(n){
        return  n>1? this.chirp(n-1)+"-chirp":"chirp"; //此处固定写为ninja.chirp,容易丢失！
    }
}

var samurai = {chirp:ninja.chirp};
ninja = {};
samurai.chirp(3)  ;// 正确！

// 隐患，对象属性名必须为chirp

var samurai2 = {chirp2:ninja.chirp};
ninja = {};
samurai2.chirp2(3)  ;// 错误！

```

> 最终方案（给匿名函数取名）
- 函数的名称仅在函数内部可见

```
var ninja = {
    chirp: function signal(n){   //给函数命名
        return  n>1? signal(n-1)+"-chirp":"chirp";
    }
}

//过时的方案

var ninja = {
    chirp: function signal(n){
        return  n>1? arguments.callee(n-1)+"-chirp":"chirp"; //此处固定写为ninja.chirp,容易丢失！
    }
}

```

















