# 特性、属性、样式  

## 特性、属性   

1. 特性（attribute） 和 属性（property）
特性是DOM构建的一个组成部分，而属性（property）是元素保持运行时信息的主要手段

```
<img src="./gsafety.jpg" alt="">
<script type="text/javascript">
    var img = document.getElementsByTagName("img")[0];
    var newSrc= "./geoserver.png";
    img.src = newSrc;
    console.log(img.src === newSrc);  //false
    console.log(img.getAttribute("src") === newSrc); //true
    console.log(img.getAttribute("src") === "./gsafety.jpg");  //false

    // img.src = "http://localhost:63342/javaScript_Ninja/ch12%E7%89%B9%E6%80%A7%E5%B1%9E%E6%80%A7%E5%92%8C%E6%A0%B7%E5%BC%8F/geoserver.png"
    // img.getAttribute("src") === "./geoserver.png"
</script>

``` 

## 特性和属性注意事项

1. 跨浏览器命名
标准浏览器下通过class获取class特性，如 box.getAttribute("class") ;  //box
标准浏览器下获取属性property ： box.className
IE下（ie7）,需要使用 box.getAttribute("className")；
IE下（ie7）,需要使用 box.className

2. 命名限制

ECMAScript 规范中指出，某些关键词不可以作为属性名称，采用替代方案，如class采用className；

特性（attribute）    |    属性（property）
 for                       htmlFor
 class                     className
 readonly                  readOnly
 maxlength                 maxLength
 rowspan                   rowSpan
 colspan                   colSpan
