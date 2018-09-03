### 					JavaScript实战进阶01

#### 一、浏览器

1.网景公司，第一款浏览器，倒闭了
2.mozilla基金会，火狐浏览器
3.微软（ie）
    兼容性问题。js、html、css浏览器翻译
    浏览器分为高级、低级浏览器
    高级：火狐、谷歌、ie8以后
    低级：ie8以下的浏览器

4.web原理

web方向：php、java、python，服务端的语言
客户端===服务端

![](D:\PythonFile\第二阶段web\1.前端两周\1805班\jsday01\web原理.png)

#### 二、js引入方式和打印方式

**1.四种引入方式**
    （1）a标签中

```
<a href="javascript:alert('集合，准备团战')">百度一下</a>
```

    （2）div中

```
<div style="width:200px; height:200px; background-color:red" onclick="alert('等等我，马上到')"></div>
```

    （3）在html页面的任何位置加入 

```
<script>js代码</script>
```

    （4） 引入外部js(在html页面的任何位置加入)

```
<script src='js.js'></script>
```

2. **三种打印方式**
       （1）alert  	弹窗打印
       （2）**console.log**('打印的内容')   	 	结合浏览器控制台查看
       （3）document.write('打印的内容')   	 往html文档中写内容

#### 三、函数

**1.全局变量和局部变量**
       (1)全局变量：直接定义的变量，全局有效
            加var和不加var都一样
       (2) 局部变量：函数体内定义的变量，只在函数体内有效
            如果局部前面有var，该变量真是一个局部变量
            如果局部前面没有var，该变量其实是一个全局变量，在函数调用之后，该变量即可随便使用
            上面知道即可，一般情况定义变量都加var
            如果局部和全局同名，优先使用局部变量
  (3)  匿名函数
        没有函数名的函数，需要将其赋给一个变量，然后变量按照函数的形式进行调用即可
 (4)   封闭空间
        将匿名函数用小括号括起来，然后在后面再加一个小括号调用这个匿名函数，称之为封闭空间
**2、数组**
    定义：array
    遍历:
        数组定义通过索引进行访问，索引从0开始
        但是数组也可以通过属性值追加属性和值，但是一般不这么使用
        遍历的时候，通过for进行遍历只能遍历索引数组，通过forin进行遍历，既可以遍历索引，又可以遍历属性
    字符串遍历
        通过索引进行遍历，索引从0开始
**3、对象**
    **三种方式：**
    （1）构造方法
    （2）通过官方创建
    （3）直接写一个对象即可
        obj = {name: '王宝强', age: '36', wife: '马蓉蓉'}
        属性的引号可以添加也可以不添加，一般就不加了
        使用时候
        obj['name']   或者  obj.name
        在js中json格式字符串和js对象相互转化的函数
        将js对象转化为json字符串
            string = JSON.stringify(obj)
        json字符串转化为js对象

```
obj = JSON.parse(string)
obj = eval('(' + string + ')')
```

**4、常用对象和函数**
  （1）类型转化  

		parseInt===将字符串转化为整型，
	
			必须以数字开头，只要碰到非数字，转化结束 ！如果以非数字开头，转化为NaN, 两个NaN不能判	
	
			断是否相等，判断是不是NaN可以使用 isNaN函数 判断是不是NaN，是返回true，不是返回false
		parseFloat===将字符串转化为浮点
	
			必须以数字开头碰到非数字立马结束，小数点不算，如果以非数字开头，转	为NaN
   （2） Math对象

```
abs ： 绝对值函数
ceil : 向上取整
floor : 向下取整
max : 取最大的值,传递过个参数，找到最大值
min : 传递多个参数，找到最小值**
pow : 求幂
random : 随机值  只能随机0-1之间的小数，如果需要随机5-10之间的数，自己实现**
round ： 四舍五入函数
```

  （3）字符串常用函数

	indexOf ： 字符串查找函数，返回查找到的字符串的第一个字母的下标，如果找不到，返回-1  
	 			类似于python里面的find
	lastIndexOf ： 字符串查找函数，找最后一次出现的位置，找不到返回-1，类似于python里面的rfind
	    	  substr : 字符串的提取  substr(start, length)  从start开始提取length个字符
	    	 replace : 字符串替换,只能替换第一个  string.replace(old, new)
	   	 	 **toLowerCase** ： 全部转化为小写
	 		  toUpperCase : 全部转化为大写
	   		 fromCharCode : 所有的大写 65-90  所有的小写 97-122  数字 48-57
	  		  split : 按照特定的字符进行切割
   （4）数组常用函数
  		  

```
		push : 给数组追加一个元素
  		  pop : 弹出最后一个元素,只能这么做
   		 shift : 弹出数组中第一个元素
  		  unshift : 数组最前面添加一个元素
    	  join : 字符串拼接  arr.join('*')  将列表里面所有的字符串按照 * 拼接
   		 reverse : 将数组逆序
  		  slice : slice(start, end)   [start, end)  左闭右开
   		 sort : 排序,如果都是数字，默认按照数字的ascii进行排序，如果想按照数字大小排序
       	 arr.sort(function (a, b) {return a > b})  从小到大排序
```

（5） 日期对象常用函数
       		

```
 getDate : 获得日期
getDay ： 获得星期几  0-6  0表示周天
getMonth ： 0-11  当前月份减一
getFullYear : 得到年份
getHours : 得到小时  24小时进制
getMinutes : 得到分钟数
 getSeconds : 得到秒数
getTime : 时间戳，毫秒数
```



        每一个都有对应的设置方法，自己看看
        创建日期对象的方式
        // 创建当前时间的时间对象
        d = new Date()
        // 根据指定的时间戳创建时间对象
        d = new Date(1534750144520)
        // 根据时间字符串创建时间对象
        d = new Date('2018/8/20 15:29:04')
        // 根据年月日时分秒值创建对象
        d = new Date(2018, 7, 20, 15, 29, 4)
**5、js简单演示**
    背景切换
    核心：页码中有一个标签，如果想给标签添加点击事件，只需要写onclick，如果想添加其它的，添加对应事件	 即可。在事件的后面就要写代码，通过js的DOM操作找到指定节点，将节点的属性修改即可
**6、获取对象**
    DOM操作，`document object modle,` 文档操作，document就是整个文档对象

```
 document.getElementById          		根据id得到指定对象(注意用id获取时getElement不带s)
	 document.getElementsByClassName  	得到对象集合，符合类名要求的都可以得到
	 document.getElementsByName			
	 document.getElementsByTagName    	根据标签名，得到对象集合
```

【例】设置设置四个div分别用上面方式获取信息并在网页console中查看信息

```
。。。。
<body>
    <div id="libai">日照香炉生紫烟,遥看瀑布挂前川</div>
    <div class="dufu">会当凌绝顶,一览众山小</div>
    <div class="dufu">安得广厦千万间,大庇天下寒士俱欢颜</div>
    <div id="song">刘备  </div>
</body>
<script>
       div1 = document.getElementById('libai')
       console.log(typeof(div1))        #输出类型是object
       
     div2 = document.getElementsByClassName('dufu')
      console.log(div2[0])         #输出第一个fufu的div,即会当凌绝顶,一览众山小
      
    div3 = document.getElementsByTagName('div')
    console.log(div3[2])   #共四个div输出第三个：即安得广厦。。。
    
    div4 = document.getElementById('song')
    console.log(div4)    #输出id是song的div,即刘备
</script>
```

**7、常用事件**
    

```
   onmouseover ：鼠标移动上去触发
    onmouseout : 鼠标离开的时候触发
    onmouseup : 鼠标按下松开的时候触发
    onmousedown : 鼠标按下的时候触发
    onmousemove : 鼠标移动的时候触发
    onclick : 点击的时候触发
    ondblclick ： 双击的时候触发
```

例：

```
<div style="width:200px; height:200px; background-color:red" onmouseover="alert('明天我要嫁给你啦')"></div>       #鼠标移到红div上会弹框显示
<div style="width:200px; height:200px; background-color:green" onmouseout="alert('后天我们要结婚')"></div>              #鼠标从绿div中移走的时候会弹框显示
```

***注：如下两个用在input框中***

```
onblur : 失去焦点
onfocus : 获取焦点
```

**8、获取、设置属性和内容**
  （1）  获取属性（点操作、中括号操作）

```
odiv.id
odiv.className      #获取到class
 odiv.style.width
odiv.style.height
odiv.style.backgroundColor
```

     例：

```
var odiv = document.getElementById('bai')
var oa = document.getElementById('lala')
console.log(odiv.style.height)
 console.log(odiv.style.backgroundColor)

console.log(odiv.innerHTML)
 console.log(odiv.innerText)
 console.log(odiv.style.width)
 console.log(odiv.style['width'])
 console.log(odiv['style']['width'])
```

 **【注】在css中带杠的属性，到js中都修改为小驼峰即可**
    （2）获取内容

```
odiv.innerHTML      获取标签里面的所有文本内容，带标签
odiv.innerText         获取标签里面的纯文本内容
```

**（3）点和中括号区别**
        能使用点的地方肯定能使用中括号，能使用中括号的地方不一定能使用点
        点后面只能跟属性名，中括号里面可以写属性名字符串，也可以写变量



	**细思极恐**
**你的对手在看书**
**你的敌人在磨刀**
**你的闺蜜在减肥**
**隔壁老王在炼腰**