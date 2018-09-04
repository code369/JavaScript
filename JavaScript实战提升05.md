### 				JavaScript实战提升05

#### 一、JQuery的选择器

注意我们用jQuery之前要引入JQuery

**1.基本**
        `:first`     `:last`   `:even`   `:odd`     `:not`       `:eq()`

**2.内容**

`contains`:内容包含某某某的节点

`has` 含有

```
【例】
找到包含’晓‘字的li标签，将样式设置为背景色为青色
$('li:contains("晓")').css('backgroundColor', 'cyan')

 找li标签，li标签里面有a的节点
 $('li:has(a)').css('backgroundColor', 'cyan')
 
 找ul标签，里面有a的节点，不论层级
 $('ul:has(a)').css('backgroundColor', 'cyan')
```

**3.属性**

标签+中括号，里面写属性名====`input[name]`

```
【例】
input[name]   #有属性name的input标签
input[name=user]    #有属性为name，并且name值为user的标签
input[name!=user]   #有属性为name，并且name值不为user的标签
input[name^=user]  #正则表示，值以user开头的

【例】属性name值以user结束的input，设置背景颜色为青色
$('input[name$=user]').css('backgroundColor', 'cyan')
```

**4.子元素**
        :first-child
        :last-child
        :nth-child

**注意==**=:eq(index)' 只匹配一个元素，而这个将为每一个父元素匹配子元素。:nth-child从1开始的，而:eq()是从0算起的

```
// 找到li标签，li是第一个儿子节点的li标签
$('li:first-child').css('backgroundColor', 'cyan')

 // 找到li标签，li是最后一个儿子节点的li标签
 $('li:last-child').css('backgroundColor', 'cyan')
 
 // 找li标签，找指定下标的li标签，这个下标是儿子节点里面的第几个
  $('li:nth-child(1)').css('backgroundColor', 'cyan')
```

#### 二、JQuery样式添加和属性获取

JQuery很多都可以连写，又称作链式操作
 **1.css({})**

通过连写可以添加一个也可以添加多个

```
 css({})
        // 可以连写-链式操作
        //修改css的两个值，背景和字体大小
        $('#lala').css('backgroundColor', 'red').css('fontSize', '30px')
        // 可以传递一个js对象，直接全部修改
        $('#lala').css({backgroundColor: 'blue', fontSize: '40px'})
```

2. **attr()**

```

        // 获取指定节点的class属性
        // console.log($('#lala').attr('class'))
        // 只能获取第一个符合要求的id属性
        // console.log($('.libai').attr('id'))
        // 通过eq选择第二个符合要求的id属性
        // console.log($('.libai:eq(1)').attr('id'))
        // 给指定节点添加属性
        // $('#lala').attr('class', 'bai').attr('name', '狗蛋')
    
```

**3.removeAttr()**

```

        // 将指定节点的属性删除
        // $('#lala').removeAttr('class')
```

4. **prop()**

```

        经常用来设置checked、selected等属性，设置的值就是true、false
        // 所有下标大于1的多选框选中
        // $('input:gt(1)').prop('checked', true)
        // 将第二个下拉框设置为默认选中
        // $('#se > option:eq(2)').prop('selected', true)
```

5. **addClass ， removeClass，  toggleClass** 

```
 addClass     
        // $('#lala').addClass('hei')
  removeClass  
        // 给指定的节点添加类名
        // $('#lala').addClass('hei')
        // 给指定的节点移除指定的节点class名  bai
        // $('#lala').removeClass('bai')
   toggleClass 
        // 有bai这个class，那就是删除这个class，没有bai这个class，那就是添加class
        // $('#lala').toggleClass('bai')
```

**6.html（），text()**

这两个是用来获取文本的两个方式，不填值是获取，添值是设置内容

```
 html()
        // 读取或者设置节点内容，和innerHTML功能相同
        // console.log($('#lala').html('醉卧沙场君莫笑,古来征战几人回'))
  text()
        读取或者设置节点内容，和innerText功能相同，但是一个是方法，一个是属性，js的是方法
    
```

**6.val()，   width() ，height()** 

```
val()
        // 读取input框里面的内容
        // console.log($('#ip').val())
        // 设置input框里面的内容
        // console.log($('#ip').val('今天中午吃什么呢？'))
    width() 
    height()  
        // 读取指定对象宽度  不带px
        // console.log($('#dudu').width())
        // 设置宽度  不带px
        // console.log($('#dudu').width(300))
        // 读取高度
        // console.log($('#dudu').height())
        // 设置高度
        // console.log($('#dudu').height(400))  
```

7. **offset()** 

   如果div是绝对定位那么一定会有一个top和left值

```

        // 获取div的top值和left值
        // console.log($('#dudu').offset().top, $('#dudu').offset().left)
```

#### 三、Js对象和JQuery对象转化

js对象和jquery对象的函数不能通用
 js对象和jquery对象相互转化

```

    // var odiv = document.getElementById('dudu')
    // js对象转化jquery对象：前面加一个$
    // console.log($(odiv).width())

    // jquery对象转化为js对象==加下标值
    // console.log($('#dudu')[0].style.width)
    // console.log($('.lala')[1].style.width)
```

#### 四、JQuery文档处理

1.**append**

**appendTo** 通过子节点调用，添加到父节点上

**prepend **通过父节点调用， 在父节点最前面添加

**prependTo** 通过子节点调用，添加到父节点最前面

```
prependTo
        // 向父节点添加子节点
        // $('#car').append('<li>本田飞度</li>')
        // 通过子节点调用，添加到父节点
        // $('<li>本田飞度</li>').appendTo($('#car'))
        // 通过父节点调用，添加到父节点的最前面
        // $('#car').prepend('<li>本田飞度</li>')
        // 通过子节点调用，添加到父节点的最前面
        // $('<li>通用别克</li>').prependTo($('#car'))
```

**after**，**before**==这两个都是兄弟节点之间的操作

```

        // 是兄弟节点关系，在mao节点后面添加一个指定节点
        // $('#mao').after('<li>铃木雨燕</li>')
        // 是兄弟节点关系，在mao节点前面添加一个指定节点
        // $('#mao').before('<li>铃木雨燕</li>')
```

**insertAfter **， **insertBefore**  

**empty** 清空指定节点里面的内容

**remove**

```

        // 清空指定节点里面的内容，节点还在
        // $('#mao').empty()
        // 原生js中：父节点.removeChild(子节点)
        // 通过子节点直接调用，删除当前节点
        // $('#mao').remove()
```



####五、JQuery筛选和查找
**1.筛选**

```
eq
        // $('li').eq(n).css('backgroundColor', 'red')
        // $('li:eq(0)').css('backgroundColor', 'red')
        // $('li:eq(' + 0 + ')').css('backgroundColor', 'red')
    first
    last
        // 第一个li   和:first 一模一样
        // $('li').first().css('backgroundColor', 'red')
        // 最后一个li   和:last 一模一样
        // $('li').last().css('backgroundColor', 'red')
    hasClass
        // 判断有没有这个class,有就返回true，没有返回false
        // console.log($('li').eq(0).hasClass('wang'))
    filter
        // 找到所有li，过滤出来 .jing 的这些li
        // $('li').filter('.jing').css('backgroundColor', 'cyan')
    slice:切片，左闭右开区间
        // 取出符合要求li里面的第0个和第1个   [start, end)
        // $('li').slice(0, 2).css('backgroundColor', 'cyan')
```

**2.查找**
**children**:儿子节点
**parent**:找自己的父节点，如果不同的标签有相同的class,那么他们分别对应的父节点都会被分别找到——不含参数:代表所有的父节点；含参数：给定指定的父节点，不再往上一级查找

```
 children
        // 所有的儿子节点
        // $('#nan').children().css('backgroundColor', 'red')
        // 儿子节点中 有 .feng 的节点
        // $('#nan').children('.feng').css('backgroundColor', 'red')
    find
        // 去子孙节点中查找所有的 .feng 的节点
        // $('#nan').find('.feng').css('backgroundColor', 'cyan')
    next
    nextAll
        // 指定对象的下一个兄弟节点
        // $('#wu').next().css('backgroundColor', 'cyan')
        // 指定对象的后面所有的节点
        // $('#wu').nextAll().css('backgroundColor', 'cyan')
    prev       指定对象的上一个兄弟节点
    prevAll    指定对象的上面所有的兄弟节点
    parent     
    parents
        // 找到当前节点的父节点
        // $('.lin').parent().css('backgroundColor', 'cyan')
        // 查找得到所有的上层节点
        // $('#qing').parents().css('backgroundColor', 'cyan')
        // 查找得到指定的上层节点
        // $('#qing').parents('div').css('backgroundColor', 'cyan')
    
    siblings
        // 查找qing节点所有的兄弟节点
        // $('#qing').siblings().css('backgroundColor', 'orange')
        // 查找qing节点所有的兄弟节点，而且是.lin的兄弟节点
        // $('#qing').siblings('.lin').css('backgroundColor', 'orange')
```

####六、事件添加
1.添加事件

```
 添加事件
 //找到的所有div都会添加点击事件
  $('div).click(function () {})
```

2.事件绑定

`on`  ` off`   `one` 

```
事件绑定
        on  off  one
        绑定事件
        $('div').on('click', test1)
        $('div').on('click', test2)
        取消事件绑定
        $('div').off('click', test2)
        // 事件只能触发一次
        $('div').one('click', test2)
```

3.事件冒泡和取消事件冒泡

```
取消冒泡
        ev.stopPropagation()
```

不存在浏览器兼容性问题
**stop Propagation**
**PreventDefault**==阻止默认行为发生

```
 阻止默认行为
        ev.preventDefault()
 获取鼠标坐标
        ev.pageX, ev.pageY
    
    
 index
        // 得到指定jquery对象在前面数组中的下标，
        // console.log($('div').index($('#heng')))
```

####七、动画

**注：fn是动画完结之后执行的代码**

```
show()
        // 参数1：动画的事件
        // 参数2：动画完毕之后执行的函数
        $('#dudu').show(5000, function () {
            alert('菊花残,满地伤')
        })
        
    hide()
        和show一样
        $('#dudu').hide(5000, fn)
        
    slidedown()
        原来不显示，动画下拉显示
        $('#dudu').slideDown(5000)
    slideup()
        原来显示，动画的上拉消失
    slideToggler()
        如果隐藏就下拉显示，如果显示就上拉消失
        
    fadeIn()
        // 慢慢的显示出来
        // $('#dudu').fadeIn(5000)
    fadeOut()
        // 慢慢的消失
        // $('#dudu').fadeOut(5000)
    fadeTo()
        // 5秒之内，透明度变为0.01
        // $('#dudu').fadeTo(5000, 0.01)
    fadeToggle()
        如果隐藏就淡入显示，如果显示就淡出消失
        
    自定义的动画效果
    animate()
        // 自定义动画
        // $('#dudu').animate({width: 1000, height: 500, opacity: 0.1}, 5000)
    stop()
        停止动画
        $('#dudu').stop()
```

####八、JQuery插件
插件库网站：www.jq22.com

#### 九、JQuery小练习

1、jquery实现全选、全不选、反选

先导入JQuery(本地或在线)

遍历：exch



2、jquery实现选项卡



3、汽车轮播

思路：（1)圆点就是li标签，所以要给li标签添加mouseover事件

(2)改img属性

overfloat:hiden超出边框的隐藏

animate(样式，时间)



4、爱奇艺轮播

opcity:1 透明度设置为1
