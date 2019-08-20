# CSS笔记02

## 属性

背景颜色：background-color

**设置背景图片**：background-image:url(路径)

- 如果和原始图片宽度大小不同，则采用平铺模式
- 设置重复显示的轴向：
  - background-repeat：no-repeat,repeat-x,reapeat-y

- 背景图片的优先级更高
- 设置图片位置：
  - background-position:
  - 参数有8个，top,bottom,left,right etc.
  - 也可以使用像素大小设置位置（eg： 30px 10px），以右上角为原点表示轴向
- background-attachment
  - scroll：图片不随着滚动条滚动
  - fixed：滚动条随着滚动条而滚动，以浏览器的位置基准
- 可以合并成一个值，附加多个属性

**设置文本**

- 控制缩进
  - text-indent
  - 值可以使用像素值（30px）
  - 可以使用2em，代表字体设置大小，即设置两个字体设置大小的缩进
- 文本对齐
  - text-align：left，center，right，justify
- 颜色：color
- 单词之间间距（通过空格进行划分，包括中文）
  - word-spacing：20px
- 字符之间的间距
  - letter-spacing:20px
- 设置字体
  - text-decoration：
  - 字体闪烁：blink
  - 横线放中间：line-through
  - 横线放上面：overline
  - 横线放下面：underline
- 控制行高，影响行之间间距：line-height：20px

**字体**

- 字体格式：
  - font-family:宋体，微软雅黑
  - 字体名称最好加上双引号
  - 优先显示宋体，当宋体无法显示时才显示微软雅黑
- 字体大小
  - font-size：20px
  - 通过像素大小，em（浏览器默认字体大小）和单词进行设置
- color：可以使用rgb进行设置 color:rgb(255,0,255);
- font-style
  - normal,italic（斜体）,oblique（倾斜的，和itlic无区别）
- 设置字体的粗细：
  - font-wight
  - 参数有：light（变细），bolder（加粗）
- 字体可以一起设置，需要按照顺序设置

**列表**

统一设置属性：list-sytle

对于无序列表ul

- 列举前面点的类型
  - list-style-type
  - circle,disc,square,none
- 将列举的点变成图片
  - list-sytle-image:url(路径);
- list-style-position
  - 文字占据多行时，显示不同的缩进格式
  - inside,outside

对于有序列表ol

- 列举前面点的类型
  - list-style-type，但是值和ul不同

display：

- 修改元素形式（块元素，行内元素）
- block，inline

## CSS单位

px,em都是相对的单位

像素根据屏幕的大小进行改变
