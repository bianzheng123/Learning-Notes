# CSS笔记03

## 盒子模型

element，border（边框），padding（内边距），margin（外边距）

盒子宽度：width + 2 * (border + padding + margin)

## 属性：

border: 10px，solid

padding

- padding-top, padding-right, padding-bottom, padding-left
- 参数可以是像素，也可以是em，也可以是百分比（相对于父元素来计算）
- 也可以直接写四个大小的值（padding：1px）（上右下左），也可以写同一个值，代表四个方向同一个值

margin

- 设置方式同padding
- 可以设置为margin: 0 auto 0 auto，这样代表左右居中，但是不会上下居中
- margin只能实现左右居中，不能上下居中

border：10px，solid，green

- 单独设置border边框时不起作用
- border-width，四个边界都可以设置
  - border-top-width
- border-style：默认值none，需要设置该值才能显示
  - 这里可以专门设置一个边的样式：border-top-style
- border-color，同border-width
- border-radius，边边角角的转弯，参数为像素值

## 相关操作

将元素设置为左右居中

- margin: 0 auto 0 auto

## 注意事项

body也是一个块元素，就有自身的外边距，内边距

通过设置body元素就可以将留白删除

每一个元素都只能存在于在其他元素的外边距外

p标签就是另外一种div标签，区别在于和div标签的盒子属性不一样

设置高度为百分比且父标签为浏览器，此时可能无法正确显示

当两个盒子具有重合（相邻）或者父子关系时，会进行合并，采用外边距最大的那个来表示外边距