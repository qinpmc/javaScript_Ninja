# 闭包

1. 内部函数的参数是包含在闭包中的；
2. 作用域之外的所有变量，即便是函数声明之后的那些声明，也都包含在闭包中；
3. 相同的作用域内，尚未声明的变量是不能提前进行引用。

```
<ul id="results"></ul>
<script>
    function assert(value, desc) {
        var li = document.createElement("li");
        li.className = value ? "pass" : "fail";
        li.appendChild(document.createTextNode(desc));
        document.getElementById("results").appendChild(li);
    }

    var outerValue = "ninja";
    var later;
    function outerFunction() {
        var innerValue = "samurai";
        function innerFunction(paramValue){
            assert(outerValue,"Inner can see the ninja");
            assert(innerValue,"Inner can see the samurai");
            assert(paramValue,"Inner can see the wakizashi");
            assert(tooLate,"Inner can see the ronin");
        }
        later = innerFunction;
    }
    assert(!tooLate,"Outer can'not see the ronin");
    var tooLate = "ronin";
    outerFunction();
    later("wakizashi");
</script>
```


