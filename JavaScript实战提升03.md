### 		JavaScript实战提升03

#### 1、DOM操作

	children    子节点  儿子节点
	parentNode  父节点

	谷歌和火狐的方式
	firstElementChild  一胎  
	lastElementChild   最后一胎
	previousElementSibling  上一个兄弟节点
	nextElementSibling      下一个兄弟节点
	
	这是ie的方式
	firstChild
	lastChild
	previousSibling
	nextSibling
	
	// 通过document可以动态的创建和删除节点
	tagName      获取对象标签的名字  大写
	createElement  创建节点
	removeChild    父节点.removeChild(子节点)
	appendChild    添加节点
		添加存在的节点，本质是移动节点
	insertBefore   添加节点   insertBefore(new, old)
	
	setAttribute :  既可以设置官方属性，又可以设置自定义属性
	getAttribute : 既可以获取官方属性，也可以获取自定义属性
	
	留言板
	山海关（锦州）、潼关、剑门关（四川盆地）、娘子关、玉门关、嘉峪关
#### 2、事件绑定和事件冒泡

	addEventListener    谷歌和火狐方式
	removeEventListener
	attachEvent         ie方式
	detachEvent

	获取事件对象
		事件ev   火狐、谷歌
		window.event   ie、谷歌
		兼容性写法：  var oevent = ev || event
	获取事件的x和y坐标
		oevent.clientX   oevent.clientY
		相对窗口左上角的坐标
	取消事件冒泡
		事件的属性和方法
		cancelBubble        ie方式、谷歌、火狐都支持
		stopPropagation()   谷歌、火狐方式
	事件源对象
		srcElement   ie、谷歌
		target       火狐、谷歌
#### 3、小知识

禁止鼠标右键
		document.oncontextmenu = function () {
			return false
		}
	超链接和事件同时触发
		事件的属性和方法
		returnValue         ie、谷歌
		preventDefault()    火狐、谷歌
		return false        ie、谷歌、火狐
	键盘事件
		document.onkeydown : 捕获用户点击的按钮
		获取按钮的编号
		oevent.keyCode

#### 3、正则对象

规则是一样的。
	单字符：.  \w  \d  \W  \s  \S  \D  [aoe]
	数量：  {m}  {m,}  {m,n}  {0,}==*  {1,}==+  {0,1}==?
    match : 正则匹配
	replace : 正则替换

#### 4、表单对象

	三种查找方法
	（1）根据id获取
	（2）document.forms  得到文档中所有的form
	（3）根据name获取
		document.formname
		获取该表单里面input框的值，假如该input框name=user
		document.formname.user.value
	submit()方法
		document.formname.submit()   谁都能提交
	js验证表单内容