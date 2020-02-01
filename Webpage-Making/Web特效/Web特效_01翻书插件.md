# Web特效_01翻书插件

## 插件内置类设置

shadow类

用于对书添加阴影

even类

对偶数页做操作

odd类

奇数，同理

p[1-9]+类

对第xxx页单独处理

## 设置图书初始化参数

```javascript
$(function () {
    function loadBook(){
        $(".flipbook").turn({
            // width: 900,
            // height: 650,
            //图片宽450，高650
            page: 1,
            acceleration:true
            //手机访问时这个设置为true
            autoCenter:true
            //设置书是否在中间，一般为true
            display:"single"
            //设置图书是单页还是双页显示，默认为double
            pages:6,
            //设置总的页数
            duration:600
            //翻页翻过去的时间，默认是600ms
            gradients:false
            //设置翻页时是否有阴影效果，默认为true
            when:{
				turned: function(ev,page,pageObj){
					console.log("第 + page + "翻过去了");
            //当页翻过去后触发事件
                                console.log("总页数" + $(".flipbook").turn("pages"));
            //使用turn获取当前的属性
                }
            },
    		//设置监听
    		direction:"rtl"
    		//设置翻页方式，默认ltr
        });
    }
    yepnope({
        test:Modernizr.csstransforms,
        yep:['../js/turn.min.js'],
        //    如果成功，就引入支持h5的css
        nope:['../js/turn.html4.min.js'],
        complete:loadBook()
    })
})
```

## js代码操作

#### 添加页

```javascript
var newPage = $(`<div style=\"background-image: url('../images/5.jpg')\"></div>`);
                $(".flipbook").turn("addPage",newPage,5);
//第一个参数表示添加页，第二个参数表示新的页对象，第三个参数表示添加到第几页
```

#### 删除页

```javascript
$(".flipbook").turn("removePage",1);
```

#### 删除所有

```javascript
$(".flipbook").turn("destroy");
```

#### 判断添加的页是否存在

```javascript
$(".flipbook").turn("hasPage",i)
```

#### 切换到上一页/下一页

```javascript
$(".flipbook").turn("previous").turn("stop");
//切换到上一页，不使用动画效果
$(".flipbook").turn("next");
//下一页
```

#### 卷页

```javascript
$(".flipbook").turn("peel","tr");
//第二个参数六个选项
//tr,tl,br,bl,r,l
//r,l只针对硬纸板
```

#### 放大/缩小

```javascript
$(".flipbook").turn("zoom",0.5,500);
//第二个参数控制放大缩小，小于1缩小，大于1放大
//第三个参数表示动画时间，单位毫秒
```

并设置内容防止拉伸、平铺

```css
.flipbook .page{
    background-repeat: no-repeat;
    background-size: 100% 100%;
}
```

实现放大/缩小的动画效果

- 使用zoom.js

zoom.js 使用注意事项
1.先进行初始化，再进行放大和缩小
2.是谁调用zoom函数，是图书的爷爷元素
3.对图书的爷爷元素必须要进行正确的宽高设置

放大时是不能翻页的，这时候需要添加翻页的按钮，并且这个翻页的按钮是固定定位

## 编辑事件

#### 使用when方式

```javascript
function loadBook(){
    $(".flipbook").turn({
        page: 1,
        //图书在开始时显示的页码
        autoCenter: true,
        pages:6,
        when:{
            turned: function(ev,page,pageObj){
                console.log("第" + page + "翻过去了");
            }
        }
    });
}
yepnope({
    test:Modernizr.csstransforms,
    yep:['../js/turn.min.js'],
    //    如果成功，就引入支持h5的css
    nope:['../js/turn.html4.min.js'],
    complete:loadBook
})
```

#### 使用bind方式

```javascript
//第一页的绑定事件
$(".flipbook").bind("first",function(){

})
//最后一页的绑定事件
$(".flipbook").bind("last",function(){

})
//当点击到最后一页/第一页时触发的事件
```

### missing

当页面缺失时触发

```javascript
//处理页面丢失事件
$(".flipbook").bind("missing",function (ev,pages) {
for(var i=0;i<pages.length;i++){
var num = pages[i];
console.log("丢失了第" + num + "页");
var newPage2 = $(`<div style=\"background-image: url('../images/` + num + `.jpg')\"></div>`);
$(".flipbook").turn("addPage",newPage2,num);
    //添加缺失的页面
}
});
```

