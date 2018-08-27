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


## 性能问题： 属性的获取和设置总比 getAttribute 和setAttribute 快

## DOM 中的id/name 膨胀
浏览器中会将表单input元素的id 、name特性作为 form 元素的属性值进行引用。

```
<form action="/" id="testForm">
    <input type="text" id="id">
    <input type="text" name="action">
</form>
<script type="text/javascript">
    window.onload = function () {
        var form = document.getElementById("testForm");
        console.log(form.id ==="testForm")  //false   form.id 为 input#id
        console.log(form.action ==="/");  //false  form.action 为 input
        console.log(form.getAttribute("id"));  //testForm
        console.log(form.getAttribute("action")); //   /

        console.log(form.getAttributeNode("action").nodeValue); //      /
    }
</script>
```

## URL 规范化造成特性属性不一致
> 访问URL属性时（如href/src/action），该URL会自动将原始值转换成完整规范的URL。

```
    <a href="性能-p251.html" id="test1"></a>
    <script type="text/javascript">
        var link = document.getElementById("test1");
        var linkHref = link.getAttributeNode("href").nodeValue;
        console.log(linkHref);  //性能-p251.html
        console.log(link.getAttribute("href"));  //性能-p251.html
        console.log(link.href);  //  http://localhost:63342/js_Ninja/ch12%E7%89%B9%E6%80%A7%E5%B1%9E%E6%80%A7%E5%92%8C%E6%A0%B7%E5%BC%8F/%E6%80%A7%E8%83%BD-p251.html
    </script>
```
## 其他问题
1. style 特性：获取 <div style="color: red"></div> 的style 特性（专指获取 "color: red"），其他浏览器均用 div.getAttribute("style");
   ie7- 使用 div.style.cssText ; 所有浏览器支持  div.style.color   // red

2. type :IE8- input元素被插入文档中后，type 特性不可变

3. 节点名称 ：html中节点名称为大写（如 HTML BODY），但XML、XHTML中可能为大小，可能为小写或组合。

## 样式的位置
1. 元素的样式信息位于DOM元素的style属性上，该信息的初始值在元素的style特性上设置的，如 style = "color:red"
   会把样式信息 保存在 样式对象上。
> 颜色信息被浏览器转换为规范化 的RGB值；color: #000 -- 转换为  rgb(0, 0, 0)
> style 对象不反映从CSS样式表继承的样式信息
> 样式属性名称，连字符改为驼峰：
    console.log(div.style.backgroundColor); //aliceblue
    console.log(div.style["background-color"]); //aliceblue

function style(ele,name.value){
    name = name.replace(/-[a-z]/ig,function(all,letter){
        return letter.toUpperCase();
    })
}

> float : 用div.style.float或 div.style.cssFloat 获取
> 像素值，元素的height、width等样式赋值时，应该带上像素单位，如 ele.style.height= "10px";
> 获取元素的尺寸

```
    <div id="div1">
        对于offsetWidth和offsetHeight，都表示当前对象的宽度/高度。
        offsetWidth与style.widtht的区别是：若对象的宽度设定值为百分百宽度，无论页面变大或变小，style.width都返回此百分比；
        而offsetWidth则返回页面中对象的宽度值而不是百分比。
    </div>
    <div id="div2" style="height: 100px;display: none">
        百分比。
    </div>
    <script type="text/javascript">
        // height/width 不指定值的话，默认为auto；此时无法获取height/width
        // 可以使用offsetHeight/offsetWidth 获取，但此值包含 border和padding
        var div1 = document.getElementById("div1"),div2=document.getElementById("div2") ;
        console.log(div1.style.height); // ""
        console.log(div1.offsetHeight); // 43

        // offsetHeight/offsetWidth 在display:none 时，取得的值为0；
        console.log(div2.style.height); // 100px
        console.log(div2.offsetHeight); // 0
    </script>
```
> 对 display:none 的元素获取offsetHeight/offsetWidth

```
        (function(){
            var PROS = {
                position:"absolute",
                visibility:"hidden",
                display:"block"
            };
            window.getDimensions = function(ele){
                var pres = {};
                for(var key in PROS){
                    pres[key] = ele.style[key]; //备份原有样式
                    ele.style[key] = PROS[key];
                };
                var result = {
                    width:ele.offsetWidth,
                    height:ele.offsetHeight
                };
                for(var key in pres){
                    ele.style[key] = pres[key];
                }
                return result;
            }
        })();
```



