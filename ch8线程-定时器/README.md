# 线程和定时器

## setTimeout 与 setInterval区别
- setTimeout中，要在前一个callback 回调执行结束并延迟 n 秒；
- setInterval 每隔n秒 尝试执行callback；不关注上一个callback是何时执行的。
- 定时器指定的时间间隔表示何时将定时器的代码添加到队列，而不是何时实际执行代码。
- 队列中已经有一个定时器代码实例时，新的定时器不会被添加到队列中。