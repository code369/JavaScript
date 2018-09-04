### 			Javascript实战提升04 

#### **一、【练】下拉框**

让两个下拉框内容左右移动

1.知识点：

（1）select标签===下拉框；**select**元素中的 **option** 标签用于定义列表中的可用选项。

（2）Document 对象方法

**getElementById()**=== 返回对拥有指定 id 的第一个对象的引用。

**getElementsByName()** ===返回带有指定名称的对象集合。

**getElementsByTagName()** ===返回带有指定标签名的对象集合。

(3) &nbsp===空格
获取可视性的宽度和高度

```
document.documentElement.clientWidth
document.documentElement.clientheight
```

（4）**appendChild()** 方法可向节点的子节点列表的末尾添加新的子节点。

**提示：**如果文档树中已经存在了 newchild，它将从文档树中删除，然后重新插入它的新位置。如果 newchild 是 DocumentFragment 节点，则不会直接插入它，而是把它的子节点按序插入当前节点的 childNodes[] 数组的末尾。你可以使用 appendChild() 方法移除元素到另外一个元素。

2.单个移动

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>下拉框实现</title>
</head>
<body>
    <select name="" id="man" size="10" multiple="1" style="width:200px;">
        <option value="">秦始皇</option>
        <option value="">汉武帝</option>
        <option value="">唐太宗</option>
        <option value="">明太祖</option>
        <option value="">毛主席</option>
    </select>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    <select name="" id="woman" size="10" multiple="1" style="width:200px;">
        <option value="">西施</option>
        <option value="">王昭君</option>
        <option value="">杨玉环</option>
        <option value="">貂蝉</option>
        <option value="">宋美龄</option>
    </select>
    <br><br><br>
    <input id="btn1" type="button" value="移动到右边" style="margin-left:40px;">
    <input id="btn2" type="button" value="移动到左边" style="margin-left:180px;">
</body>
</html>
<script>
var oman = document.getElementById('man')
var owoman = document.getElementById('woman')
// 移动到右边的代码
var obtn1 = document.getElementById('btn1')
obtn1.onclick = function () {
    // 得到选中框的下标
    // alert(oman.selectedIndex)
    var index = oman.selectedIndex
    // 得到选中的option框
    var ooption = oman.options[index]
    // 将选中的框，添加到owoman中
    owoman.appendChild(ooption)
}
// 移动到左边的代码
var obtn2 = document.getElementById('btn2')
obtn2.onclick = function () {
    // 得到选中框的下标
    // alert(oman.selectedIndex)
    var index = owoman.selectedIndex
    // 得到选中的option框
    var ooption = owoman.options[index]
    // 将选中的框，添加到owoman中
    oman.appendChild(ooption)
}

</script>
```

3.优化：实现多选的左右移动

这里我们可以将js代码中添加遍历内容

```
<script>
var oman = document.getElementById('man')
var owoman = document.getElementById('woman')
// 移动到右边的代码
var obtn1 = document.getElementById('btn1')
obtn1.onclick = function () {
    // console.log(oman.selectedIndex)
    // 得到所有的options
    var options = oman.options
    // 遍历这个数组，依次得到每个option的状态
    // 啦啦  嘟嘟  嘻嘻
    //  0    1    2
    for (var i = 0; i < options.length; i++) {
        // 得到当前option框的状态，选中为true，没有选中为false
        // console.log(options[i].selected)
        if (options[i].selected) {
            owoman.appendChild(options[i])
            i--
        }
    }
}
// 移动到左边的代码
var obtn2 = document.getElementById('btn2')
obtn2.onclick = function () {
    var options = owoman.options
    // 遍历这个数组，依次得到每个option的状态
    // 啦啦  嘟嘟  嘻嘻
    //  0    1    2
    for (var i = 0; i < options.length; i++) {
        // 得到当前option框的状态，选中为true，没有选中为false
        // console.log(options[i].selected)
        if (options[i].selected) {
            oman.appendChild(options[i])
            i--
        }
    }
}

</script>
```

#### 二、【练】倒计时

距离国庆节还有多少天、小时、分钟、秒

思路：根据时间戳来计算天数，小时，分钟和秒数-

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>倒计时</title>
</head>
<body>
    <h1 id="dao"></h1>
</body>
</html>
<script>
var odao = document.getElementById('dao')
// 获取国庆节的时间
var oqing = new Date('2018-8-23 10:16:00')
// 得到国庆节的时间戳
var oqingcuo = oqing.getTime()
var timer = null
function demo() {
    // 每次都要获取当前的时间对象
    var onow = new Date()
    // 得到当前的时间戳
    var onowcuo = onow.getTime()
    if (oqingcuo <= onowcuo) {
        clearInterval(timer)
    }
    // 得到两个时间戳的差值
    var dist = (oqingcuo - onowcuo) / 1000
    // 将这个差值你要给我计算出来有多少天、多少小时、多少分钟、多少秒
    // 首先计算天数   3600*24=86400  90000
    var day = parseInt(dist / 86400)
    // 计算除了天之后剩下的时间
    dist = dist % 86400
    // 计算小时
    var hour = parseInt(dist / 3600)
    dist = dist % 3600
    // 计算分钟
    var minute = parseInt(dist / 60)
    dist = dist % 60
    var second = parseInt(dist)
    odao.innerHTML = '距离下课还有===' + day + '天' + hour + '小时' + minute + '分钟' + second + '秒'
}
timer = setInterval(demo, 1000)
</script>
```

三、【练】让图片在网页中飘动（到边界要反弹不消失）

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>飘动广告</title>
    <style>
    div {
        position: fixed;
        top: 0px;
        left: 0px;
    }
    </style>
</head>
<body>
    <div id="girl">
        <img src="meinv.jpg" alt="" height="300" width="200">
    </div>
</body>
</html>
<script>
var odiv = document.getElementById('girl')
// 定义偏移量
var offset_top = 10
var offset_left = 10
// 兼容性写法获取非行内样式
function getStyle(obj, name) {
    return obj.currentStyle ? obj.currentStyle[name] : getComputedStyle(obj, null)[name]
}

// 获取可视区的宽度和高度
// 获取宽高的时候，要看有没有DTD的说明，如果有，使用documentElement，如果没有，使用body
var clientWidth = document.documentElement.clientWidth
var clientHeight = document.documentElement.clientHeight
// console.log(clientWidth, clientHeight)

setInterval(function () {
    // 动态的修改top和left值
    // 得到你的top和left值
    var top = parseInt(getStyle(odiv, 'top'))
    var left = parseInt(getStyle(odiv, 'left'))
    top += offset_top
    left += offset_left
    // 判断top或则left有没有到达边界
    if (top + 300 > clientHeight || top < 0) {
        offset_top = -offset_top
    }
    if (left + 200 > clientWidth || left < 0) {
        offset_left = -offset_left
    }

    // 再将修改后的值赋值过去
    odiv.style.top = top + 'px'
    odiv.style.left = left + 'px'
}, 5)
</script>
```

#### 四、【练】创建一个div让div跟着鼠标移动

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>跟随鼠标移动</title>

</head>
<body>
    <!-- <div id="girl" style="position: absolute; top: 0px; left: 0px; background-color: red; width: 300px; height: 300px;"> -->
    <div id="girl" style="position: absolute; top: 0px; left: 0px;">
        <img src="meinv.jpg" alt="" height="300" width="200">
    </div>
</body>
</html>
<script>
var odiv = document.getElementById('girl')
odiv.onmousedown = function (ev) {
    var oevent = ev || event
    // 首先得到图片的左边距和上边距
    var divleft = parseInt(odiv.style.left)
    var divtop = parseInt(odiv.style.top)

    // console.log(divleft, divtop)
    // 在这获取鼠标点击的时候，左边的间距和上边的间距
    var offsettop = oevent.clientY - divtop
    var offsetleft = oevent.clientX - divleft
    // console.log(offsettop, offsetleft)

    document.onmousemove = function (ev) {
        var oe = ev || event
        console.log(ev.clientX, ev.clientY)
        // 修改div的top和left值
        odiv.style.top = (oe.clientY - offsettop) + 'px'
        odiv.style.left = (oe.clientX - offsetleft) + 'px'
    }
    // 防止默认的行为发生
    return false
}

odiv.onmouseup = function () {
    // 设置为空，松开鼠标图片就不会跟着鼠标走了
    document.onmousemove = null
}


</script>
```

#### 五、全选和反选的操作

1.知识点:

(1)**checked** 属性设置或返回 checkbox 是否应被选中。

格式：

```
checkboxObject.checked=true|false
```

该属性保存了 checkbox 的当前状态，不管何时，这个值发生变化的时候，onclick 事件句柄就会触发（也可能触发 onchange 事件句柄）。

(2)

| [document.getElementsByClassName()](http://www.runoob.com/jsref/met-document-getelementsbyclassname.html) | 返回文档中所有指定类名的元素集合，作为 NodeList 对象。 |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| [document.getElementById()](http://www.runoob.com/jsref/met-document-getelementbyid.html) | 返回对拥有指定 id 的第一个对象的引用。                 |
| [document.getElementsByName()](http://www.runoob.com/jsref/met-doc-getelementsbyname.html) | 返回带有指定名称的对象集合。                           |
| [document.getElementsByTagName()](http://www.runoob.com/jsref/met-document-getelementsbytagname.html) | 返回带有指定标签名的对象集合。                         |

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>全选</title>
</head>
<body>
    <li><input type="checkbox">梅西</li>
    <li><input type="checkbox">c罗</li>
    <li><input type="checkbox">内马尔</li>
    <li><input type="checkbox">李哥</li>
    <li><input type="checkbox">詹姆斯</li>
    <li><input type="checkbox">罗纳尔多</li>
    <li><input type="checkbox">库里</li>
    <li><input type="checkbox">乔治</li>
    <li><input type="checkbox">维斯布鲁克</li>
    <li><input type="checkbox">爱新觉罗姚明</li>
    <button>全选</button>
    <button>全不选</button>
    <button>反选</button>
</body>
</html>
<script>
var ainputs = document.getElementsByTagName('input')
var abtns = document.getElementsByTagName('button')
abtns[0].onclick = function () {
    // 遍历所有的input，将每一个input的checked属性设置为true
    for (var i = 0; i < ainputs.length; i++) {
        ainputs[i].checked = true
    }
}

abtns[1].onclick = function () {
    // 遍历所有的input，将每一个input的checked属性设置为true
    for (var i = 0; i < ainputs.length; i++) {
        ainputs[i].checked = false
    }
}

abtns[2].onclick = function () {
    // 遍历所有的input，将每一个input的checked属性设置为true或者false
    for (var i = 0; i < ainputs.length; i++) {
        ainputs[i].checked = !ainputs[i].checked
        // if (ainputs[i].checked) {
        //     ainputs[i].checked = false
        // } else {
        //     ainputs[i].checked = true
        // }
    }
}
</script>
```

#### 六、offset操作

**offsetWidth, offsetHeight=**=可以直接获取到div的宽度和高度，而且是不带px， 并且样式无论在哪都可以获取到，这两个属性是只读属性

**offsetTop, offsetLef**t可以直接获取到div的距离浏览器上边的距离和距离浏览器左边的距离，而且是不带px， 并且样式无论在哪都可以获取到，这两个属性是只读属性

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>offset属性</title>
    <style>
    div {
        width: 400px;
        height: 500px;
        background-color: cyan;
        position: absolute;
        top: 100px;
        left: 200px;
    }
    </style>
</head>
<body>
    <div id="dudu"></div>
</body>
</html>
<script>
var odiv = document.getElementById('dudu')
// 可以直接获取到div的宽度和高度，而且是不带px， 并且样式无论在哪都可以获取到，这两个属性是只读属性
console.log(odiv.offsetWidth, odiv.offsetHeight)
// 可以直接获取到div的距离浏览器上边的距离和距离浏览器左边的距离，而且是不带px， 并且样式无论在哪都可以获取到，这两个属性是只读属性
console.log(odiv.offsetTop, odiv.offsetLeft)
</script>
```

输出

400,500

100,200

#### 七、滚动事件==**onscroll**

```
<script>
// 滚动就会触发这个事件
window.l = function () {
    // 查看网页卷起的高度，如果是在DTD下，documentElement获取，如果不在，通过body获取
    console.log(document.documentElement.scrollTop)
}
</script>
```

#### 八、吸顶条

1.可以直接获取到div的宽度和高度，而且是不带px， 并且样式无论在哪都可以获取到，这两个属性是只读属性

```
offsetWidth
offsetHeight
```

2. 可以直接获取到div的距离浏览器上边的距离和距离浏览器左边的距离，而且是不带px， 并且样式无论在哪都可以获取到，这两个属性是只读属性

```
 offsetTop
 offsetLeft
```

#### 九.自动播放选项卡**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>自动播放选项卡</title>
    <style>
        .box {
            width: 1000px;
            border: 1px solid gray;
            margin: 0 auto;
        }
        button {
            width: 170px;
            height: 100px;
            font-size: 20px;
            background-color: pink;
            margin-left: 55px;
            display: inline-block;
        }
        .box > div {
            width: 970px;
            height: 600px;
            font-size: 50px;
            background-color: yellow;
            margin-left: 15px;
            margin-top: 50px;
            display: none;
        }
        .box > .active {
            font-size: 30px;
            background-color: blue;
        }
        .box > .show {
            display: block;
        }
        </style>
</head>
<body>
    <div class="box">
        <button class="active">国产电影</button>
        <button>韩日电影</button>
        <button>欧美电影</button>
        <button>其他电影</button>
        <div class="show">霸王别姬、卧虎藏龙、大话西游、东邪西毒、无间道、功夫</div>
        <div>釜山行、汉江怪物、奥特曼、灌篮高手、热血高校、午夜凶铃</div>
        <div>肖申克的救赎、阿甘正传、敢死队、泰坦尼克号、这个杀手不太冷、盗梦空间</div>
        <div>三傻大闹宝莱坞、摔跤吧、小萝莉的猴神大叔、厕所英雄</div>
    </div>
</body>
</html>
<script>
// 首先找到最外层的box
var obox = document.getElementsByClassName('box')[0]
// 找到所有的button
var abtns = obox.getElementsByTagName('button')
// 找到所有的div
var adivs = obox.getElementsByTagName('div')

// 记录要切换的div获取按钮的下标
var number = 0

// 循环给每一个button添加点击事件
for (var i = 0; i < abtns.length; i++) {
    abtns[i].index = i
    abtns[i].onclick = function () {
        // 首先清空所有的class
        for (var j = 0; j < abtns.length; j++) {
            abtns[j].className = ''
            adivs[j].className = ''
        }
        // 然后给指定的添加class
        this.className = 'active'
        adivs[this.index].className = 'show'
        // 将number更新一下
        number = this.index
    }
}

// 自动播放代码
function next() {
    // 显示下一个需要显示的button和div
    number++
    number %= 4
    // 先清掉所有的样式
    for (var j = 0; j < abtns.length; j++) {
        abtns[j].className = ''
        adivs[j].className = ''
    }
    abtns[number].className = 'active'
    adivs[number].className = 'show'
}
var timer = setInterval(next, 1000)

// 如果鼠标放到box上面，将定时器销毁，鼠标离开box的时候，重新创建定时器自动播放
obox.onmouseover = function () {
    clearInterval(timer)
}
obox.onmouseout = function () {
    timer = setInterval(next, 1000)
}
</script>
```

#### 十.JQuery

write less,do more!

**1.JQuery是什么?**

 官网的解释为 jQuery是一个快速、小型、功能丰富的JavaScript库。它使HTML文档遍历和操作、事件处理、动画和Ajax等工作变得更加简单，并且具有在多个浏览器之间工作的易于使用的API。结合了通用性和可扩展性，jQuery改变了数百万人编写JavaScript的方式。

jQuery is a fast, small, and feature-rich JavaScript library. It makes things like HTML document traversal and manipulation, event handling, animation, and Ajax much simpler with an easy-to-use API that works across a multitude of browsers. With a combination of versatility and extensibility, jQuery has changed the way that millions of people write JavaScript.  

**2.版本常识**

目前jQuery有三个大版本：

```
1.x：兼容ie678,使用最为广泛的，官方只做BUG维护，功能不再新增。因此一般项目来说，使用1.x版本就可以了，最终版本：1.12.4 (2016年5月20日)
2.x：不兼容ie678，很少有人使用，官方只做BUG维护，功能不再新增。如果不考虑兼容低版本的浏览器可以使用2.x，最终版本：2.2.4 (2016年5月20日)
3.x：不兼容ie678，只支持最新的浏览器。除非特殊要求，一般不会使用3.x版本的，很多老的jQuery插件不支持这个版本。目前该版本是官方主要更新维护的版本。
```

1.X大版本下，细分版本非常多，各个版本的函数都会有一定的差异。网上看到的很多教程大多是1.x版本的。jquery官方手册：http://api.jquery.com/
维护ie678是一件头疼的事情，一般我们都会额外加载一个css和js单独处理。值得庆幸的是使用这些浏览器的人也逐步减少，电脑端用户已经逐步被移动端用户所取代，如果没有特殊要求的话，一般都会选择放弃对ie678的支持。

**【注意】**

压缩版本：后缀.min.js 一行代码全部搞定的形式

非压缩版本：后缀.js

下载网址：www.bootcdn.cn/jquery

**3.使用方式：**

两种使用方式可以本地使用，也可以引入在线文件

```
 可以本地使用
  <script src="jquery/jquery-1.11.3.min.js"></script>
  可以引入网络文件使用
   <script src="https://cdn.bootcss.com/jquery/3.3.1/jquery.min.js"></script>
```

**4.为什么推荐使用jQuery而不写原生JS**

 因为jQuery对象有更多的属性和方法, 能够用更少的代码做更多的事情,而且jQuery对象的方法使用灵活且没有浏览器兼容性问题

**5.$既是一个对象也是一个函数**

```
当$作为函数时有以下四种最常用的用法:
(1). 如果$函数的参数是一个函数, 传入的函数是页面加载完成时要执行的回调函数
(2). 如果$函数的参数是选择器字符串, 那么$函数会返回代表元素的jQuery对象(其本质是一个数组)
(3). 如果$函数的参数是标签字符串, 那么$函数会创建该标签并返回对应的jQuery对象
(4). 如果$函数的参数是原生JavaScript对象(DOM), 那么$函数将该对象处理成jQuery对象
```

**6.选择器**
        jquery通过选择器就可以找到指定的节点
            id、class、标签、层级
        基本
            :first   第一个
            :last    最后一个
            :even    偶数下标
            :odd     奇数下标
            :eq()    等于哪个下标
            :gt()    大于哪个下标
            :lt()    小于哪个下标

```
$(function () {
    #jquery代码都写到这里
    $('#lala').css('backgroundColor', 'red')
    $('.star').css('backgroundColor', 'yellow')
    $('li').css('backgroundColor', 'blue')
    $('.song > li').css('backgroundColor', 'cyan')

    #第一个
    $('li:first').css('backgroundColor', 'cyan')
    #最后一个
    $('li:last').css('backgroundColor', 'cyan')
   # 偶数下标的
    $('li:even').css('backgroundColor', 'cyan')
   # 奇数下标的
    $('li:odd').css('backgroundColor', 'cyan')
    #等于1的
    $('li:eq(1)').css('backgroundColor', 'cyan')
   # 大于2的
    $('li:gt(2)').css('backgroundColor', 'cyan')
    #小于2的
    $('li:lt(2)').css('backgroundColor', 'cyan')
})
</script>
```

