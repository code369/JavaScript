### 					JavaScript实战进阶02

#### 一、添加事件

**1.添加事件方式**（以点击事件为例）

（1）直接添加

```
<body>
    <div style="width:200px; height:200px; background-color:red" onclick="alert('这是一个div')"></div>   #在div中添加了点击事件
</body>
```

（2）js中写一个函数，css中直接调用

```
<body>
    <div style="width:200px; height:200px; background-color:blue" onclick="test()"></div>
    </body>                                        #电机的时候调用test()方法
<script>
function test() {
    console.log('花田里犯了错,说好,破晓前忘掉')
}
<script>                                          #在js中声明一个test函数
```

（3）js中获取节点，在js中添加事件内容

```
var odiv = document.getElementById('div')
 odiv.onclick = function () {
     console.log('遥远的东方有一条龙')
}
```

```
odiv.onclick = test    这种直接用（2)中的方法也可以
```

**2.显示隐藏图片**
	操作div的display属性，在block和none之间切换即可
**3.this使用**
	在匿名函数中的this就是当前对象
	在onclick=demo(this)  就是当前节点
	修改内容
	this.innerHTML = 'xxx'

```
<script>
    // 点击div，将宽度有200px修改为400px
    var odiv = document.getElementsByClassName('tang')[0]
    odiv.onclick = function () {
        console.log(this)
        // this就是odiv
        this.style.width = '400px'
        // 给div添加内容
        this.innerHTML = '秦时明月汉时关,万里长征人未还,但使龙城飞将在,不教胡马度阴山'
    }

    function demo(obj) {
        // 这里面的this是window，在js里面写的所有的函数都是window的函数，调用demo其实就是  window.demo()
        console.log(this)
        // var odiv = document.getElementsByClassName('tang')[1]
        obj.style.height = '400px'
    }
</script>
```

**4.切换背景色**

```
<body>
    <div id="bai" style="width:300px; height:300px; background-color:red;"></div>
</body>
</html>
<script>
var odiv = document.getElementById('bai')
odiv.onclick = function () {
    // 先获取div的背景色
    color = this.style.backgroundColor
    if (color == 'red') {
        this.style.backgroundColor = 'yellow'
    } else {
        this.style.backgroundColor = 'red'
    }  
}
```

**5.表单内容控制**

	<body>
	    <input id="ip" type="text" value="请输入用户名">
	    <input type="text" value="请输入用户名" onfocus="cleara(this)" onblur="recover(this)">
	</body>
	</html>
	<script>
	    // clear是关键字，不能使用函数名
	function cleara(obj) {
	    // console.log('clear')
	    if (obj.value == "请输入用户名") {
	        obj.value = ''
	    }
	}
	function recover(obj) {
	    if (obj.value == '') {
	        obj.value = '请输入用户名'
	    }
	}
	var oinput = document.getElementById('ip')
	oinput.onfocus = function () {
	    // 判断要不要清空
	    if (this.value == "请输入用户名") {
	        this.value = ''
	    }
	}
	oinput.onblur = function () {
	    // 判断内容是不是为空，如果为空变成下面这个
	    if (this.value == '') {
	        this.value = '请输入用户名'
	    }
	}
	</script>	

#### 二、onload函数

window的事件，windows.onload = function () {}  是在整个文档加载完毕之后执行，但是自己写的onclick的点击函数不能写到onload里面，因为内部函数只能在内部使用，不能再外部使用
	如果实在是想用，
		window.lala = function () {}

#### 三、选项卡

实现点击一个按钮，都会对应一个div

display的几个常用值

| none   | 此元素不会被显示。                                   |
| ------ | ---------------------------------------------------- |
| block  | 此元素将显示为块级元素，此元素前后会带有换行符。     |
| inline | 默认。此元素会被显示为内联元素，元素前后没有换行符。 |

```

```

实例1

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>选项卡</title>
    <style>
    button {
        width: 200px;
        height: 100px;
        font-size: 40px;
        background-color: pink;
        margin-left: 50px;
        display: inline-block;
    }
    div {
        width: 970px;
        height: 600px;
        font-size: 50px;
        background-color: yellow;
        margin-left: 50px;
        margin-top: 50px;
        display: none;
    }
    .active {
        font-size: 50px;
        background-color: blue;
    }
    .show {
        display: block;
    }
    </style>
</head>
<body>
    <button class="active">王宝强</button>
    <button>马蓉</button>
    <button>王助理</button>
    <button>啤教授</button>
    <div class="show">王宝强、王宝强、王宝强、王宝强、王宝强、王宝强</div>
    <div>马蓉、马蓉、马蓉、马蓉、马蓉、马蓉</div>
    <div>王助理、王助理、王助理、王助理、王助理、王助理</div>
    <div>啤教授、啤教授、啤教授、啤教授</div>
</body>
</html>
<script>
// 得到所有的button
var abuttons = document.getElementsByTagName('button')
var adivs = document.getElementsByTagName('div')
// 循环button数组，给里面每一个button添加点击事件
for (var i = 0; i < abuttons.length; i++) {
    // 给指定的button手动添加一个属性，用来保存是第几个button
    abuttons[i].index = i
    abuttons[i].onclick = function () {
        // 首先清掉所有button和div上面的class
        for (var j = 0; j < abuttons.length; j++) {
            abuttons[j].className = ''
            adivs[j].className = ''
        }
        // 给指定的button添加样式
        this.className = 'active'
        // console.log(i)
        // 给指定的div添加样式
        adivs[this.index].className = 'show'
    }
}
</script>
```

实例二

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>选项卡</title>
    <style>
    button {
        width: 200px;
        height: 100px;
        font-size: 40px;
        background-color: pink;
        margin-left: 50px;
        display: inline-block;
    }
    div {
        width: 970px;
        height: 600px;
        font-size: 50px;
        background-color: yellow;
        margin-left: 50px;
        margin-top: 50px;
        display: none;
    }
    .active {
        font-size: 50px;
        background-color: blue;
    }
    .show {
        display: block;
    }
    </style>
</head>
<body>
	<!--默认显示第一个div,dudu函数在js中声明-->
    <button class="active" onclick="dudu(this, 0)">周杰伦</button>
    <button onclick="dudu(this, 1)">王力宏</button>
    <button onclick="dudu(this, 2)">张学友</button>
    <button onclick="dudu(this, 3)">刘德华</button>
    <div class="show">菊花台、千里之外、七里香、霍元甲、听妈妈的话、稻香、双节棍、简单爱</div>
    <div>花田错、龙的传人、唯一</div>
    <div>慢慢、吻别、一千个伤心的理由</div>
    <div>谢谢你的爱、冰雨、天意、忘情水</div>
</body>
</html>
<script>
    // 得到所有的button
    var abuttons = document.getElementsByTagName('button')
    // 得到所有的div
    var adivs = document.getElementsByTagName('div')
    function dudu(obj, index) {
        // 先将所有的button的class属性设置为空，再给指定的添加
        for (var i = 0; i < abuttons.length; i++) {
            abuttons[i].className = ''
            adivs[i].className = ''
        }
        // 给指定的button添加样式
        obj.className = 'active'
        // 给指定的div添加样式
        adivs[index].className = 'show'
    }
</script>
```



#### 四、定时器

定时器：分为两种，一种是周期性定时器，一种是一次性定时器
	周期性：每隔5s执行一次函数
	一次性：几秒之后执行一次函数，执行完毕定时器结束
		var timer = setTimeout(fn, 5000)
		5000ms之后执行fn一次。然后结束
		销毁定时器   clearTimeout(timer)
	计数器
	图片消失

#### 五、获取非行内样式

IE浏览器获取非行内样式方式
		obj.currentStyle['name']
	火狐和谷歌获取方式
		getComputedStyle(odiv, null)['width']
	获取非行内样式的兼容性写法
	function getStyle(obj, name) {
		return obj.currentStyle ? obj.currentStyle[name] : getComputedStyle(obj, null)[name]
	}

#### 六、BOM操作

window.setTimeout,window.setInterval
	window.alert\window.confirm
	window.open
	window.history(back、go)
		history.go(1)   去往前一个网址
		history.go(2)   去往后一个网址
		history.back()  倒退一个网址
	location  
		href : 读取得到当前的url，设置跳转到指定的url
		reload() : 刷新整个页面

#### 七、DOM操作

	children
	parentNode
	firstElementChild
	lastElementChild
	previousElementSibling
	nextElementSibling
	
	firstChild
	lastChild
	previousSibling
	nextSibling
	
	tagName
	createElement
	removeChild
	appendChild
	insertBefore 
	
	setAttribute  getAttribute
#### 八、select下拉框和oninput事件

	onchange : 事件，用户点击下拉框触发
	selectedIndex : 用户点击的option的下标，下标从0开始
	options : osel.options 可以得到所有的option对象，这是一个数组
	input框的oninput事件，只要内容改变，就会触发