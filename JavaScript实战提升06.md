### 		JavaScript06

#### 一、Ajax

**1.简介**

1,Ajax--异步Javascript和XML(Asynchronous Javascript And XML)

	**优势：异步请求，局部刷新！实现动态加载**
	XML--可扩展标签语言：说明
	（1)必须要有根标签，每个标签要有开始要有结束
	（2）属性要用双引号
	Html--超文本标签语言



**2.我们是怎么上网的（请求---响应）**

(1)客户端：浏览器，前端（html、css、js、jquery）
		服务端：现成的，比如百度、csdn等，后端（php、java、python）
	
(2)上网：上网就是客户端向服务端发送请求，然后获取到服务端数据的过程
		你是通过url的切换实现的，url就是网址，来得到不同的内容

（3)ajax：在不刷新整个页面的前提下，完成了和服务端的交互，也就更新了网页里面的内容，一般都是局部更	新,在不中断用户体验的前提下从服务器获取数据为用户提供更好的 体验

```
（a）浏览器在后台向服务器发出异步请求（用js代码）
---异步请求（在后台执行不中断用户体验）
（b）服务器向浏览器返回新的数据（xml)
[xml是早年间异构系统之间交换数据的事实标准，非官方要求]
```

**3.应用:**

	nba直播，文字直播，用户注册，不更新页面加载下一页数据

**4.使用方式：**

前后端交互方式pc端两种：GET;POST  移动端：get、post、put、delete等

```
HTTP(s)协议的请求有多种请求命令
浏览器在正常情况下只能发出get或post请求，将来我们在项目中可能用到的HTTP请求命令包括以下5个:
	 - GET: 从服务器获取资源
	 - POST: 向服务器提交资源
	  - DELETE: 从服务器删除资源
	 - PUT / PATCH: 更新服务器上的资源
```

（1）方式一：原生JS实现

```
<script>
// 原生的js实现ajax的技术
// 创建对象,
// XMLHttpRequest是高级浏览器创建ajax对象的方式
// IE8以下的创建方式不一样，只需了解即可
var xhr = new XMLHttpRequest()
// 和后端进行交互，交互的方式有两种，pc端：get、post  移动端：get、post、put、delete等
// 发送get请求 
// 参数1：请求方式
// 参数2：处理这个请求的文件，或者url
// 这样就将请求发送过去了
 xhr.open('get', 'url')
 xhr.send()

// post方式如何发送
xhr.open('post', 'url')
// 发送post，必须要添加这个东西
xhr.setRequestHeader('content-type', 'application/x-www-form-urlencoded')
// 在发送send的时候，需要将要传递的参数写进来
xhr.send('name=狗蛋&password=123')

// 服务端返回数据给你，要使用下面的代码
// ajax在发送请求的时候，状态会改变，会触发这个事件
xhr.onreadystatechange = function () {
    // 4是固定的，代表的意思是请求发送成功
    if (xhr.readyState == 4) {
        // 当响应也成功的时候，就可以获取数据了,去判断响应状态码  404
        if (xhr.status == 200) {
            // 获取响应的内容
            var content = xhr.responseText
            // 响应内容一般都是json格式的字符串
            // 你的工作就是解析json字符串，将内容填充到html中
            // 首先将json格式字符串转化为js对象
            var obj = JSON.parse(content)
            // var obj = eval('(' + content + ')')
        }
    }
}
</script>
```

（2）方式2：JQuery封装好的函数

**5、交互（原生为例）**

```
<body>
    用户名:<input type="text" name="user" id="user">
    <br>
    会员等级:<input type="text" name="level" id="level">
    <br>
    会员余额:<input type="text" name="money" id="money">
    <br>
    会员年限:<input type="text" name="year" id="year">
    <br>
    <button id="btn">点我获取内容</button>
</body>
</html>
<script>
// 获取按钮
var obtn = document.getElementById('btn')
// 找到每一个input
var ouser = document.getElementById('user')
var olevel = document.getElementById('level')
var omoney = document.getElementById('money')
var oyear = document.getElementById('year')
// 添加点击事件
obtn.onclick = function () {
    // 和服务端交互, 创建ajax对象来交互
    var xhr = new XMLHttpRequest()
    xhr.open('get', 'ziliao0.php')
    xhr.send()

    xhr.onreadystatechange = function () {
        if (xhr.readyState == 4) {
            if (xhr.status == 200) {
                // console.log(xhr.responseText)
                // 将其转化为js对象
                obj = JSON.parse(xhr.responseText)
                ouser.value = obj.name
                olevel.value = obj.level
                omoney.value = obj.money
                oyear.value = obj.year
            }
        }
    }
}
</script>
```

**6.用户注册（用JQuery封装的Ajax）**

jQuery封装了多个Ajax请求方法：

```

	//-$.ajax():灵活强大（强烈推荐使用）
	//-$.getJSON():简单好用
```

[例】根据注册名判断是否已经被注册

失去焦点blur()

```
<script>
$(function () {
    $('#user').blur(function () {
        // 通过ajax将内容传递给服务端，服务端判断之后，给你个状态，你再去对应的修改你的内容
        $.ajax({
            type: "POST",
            url: "zhuce.php",
            data: "name=" + $(this).val(),
            success: function(msg){
                // msg就是服务端给你的内容
                var obj = JSON.parse(msg)
                if (obj.state == 1) {
                    $('#usertip').html('√').css('backgroundColor', 'green')
                } else {
                    $('#usertip').html('该用户已经注册').css('backgroundColor', 'red')
                }
            }
        });
    })
})
</script>
```

#### 二、Bootstrap

网站：bootstrap中文文档https://v3.bootcss.com/

**1.什么是Bootstrap**

	Bootstrap 是最受欢迎的 HTML、CSS 和 JS 框架，用于开发响应式布局、移动设备优先的 WEB 项目。
**2、如何实现pc端和手机端显示的都非常漂亮？**
	（1）布局两套，样式，大公司都是这么做的，淘宝、京东
	（2）响应式布局，根据设备的变化，来改变你的尺寸

**3、响应式布局**

（1）、不能使用px布局。rem，相对单位，是用来相对于html字体的
	   html {font-size: 20px;}
	 在你的页面中  1rem = 1*20px;   2rem = 40px;   0.5rem = 10px;
（2)、使用框架，比如bootstrap

