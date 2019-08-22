# HTML5笔记04

## 框架

使用框架则直接在```<html></html>```里面写东西，不需要加上```<body></body>```或者```<title></tile>```标签

```<frameset></frameset>```代表框架

- ```<frame/>```用于添加html文件

## 相关操作

嵌套切分

- 在原来应该加```<frame/>```标签的地方添加新的```<frameset></frameset>```

`<frameset rows="25%,75%">`

​	`<frame src="frame_a.html"/>`

​	`<frameset cols="25%,75%">`

​		`<frame src="frame_b.html"/>`

​		`<frame src="frame_c.html"/>`

​	`</frameset>`

`</frameset>`

后台管理系统的切屏操作

- 对目标切屏地点设定name（假设name内容为N1）
- 对于包含链接的网页设置target为N1，href为链接的网页"xxxx.html"
- 则点击链接，目标的切屏地点就会切换成"xxxx.html"，而不是包含链接的网页被切换成“xxxx.html”
- 这个用于后台的切屏操作

## 属性和参数

框架```<frameset rows="25%,75%" cols=""></frameset>```

- rows指的是上下划分，里面填写划分的内容，将网页分成若干小的网页
- cols代表垂直切分
- 这里的比例可以写多个
- 用```*```代表剩余的百分比
- ```<frame src="" name=""/>```
  - src用来表示其他的网页的位置
  - name表示这个框架的名字

## 注意事项

框架用于后台管理系统（给管理员看的）