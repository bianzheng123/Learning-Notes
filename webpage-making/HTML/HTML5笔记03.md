# HTML5笔记03

## 标签

以下都是在```<body></body>```标签下面进行的

每一个输入框都需要用```<form></form>```括起来，通过```<form></form>```查看是否为同一个表单

- ```<input type=""/>```：文本输入框，按钮，单选框，多选框
- ```<select></select>```：下拉列表
  - ```<option></option>```可以选择的项

- ```<textarea></textarea>```：文本域，用于输入大量文本



## 相关操作

设置单选框

- 这里使用性别作为举例
  - ```男<input type="radio" name="sex" value="man"/> 女<input type="radio" name="sex" value="woman"/>```
- 设置name为相同的参数即可，这样可以将按钮选成同一类别
- 在传参时需要特定给一个value

设置多选框

- 将type设置为checkbox
- name设置为同一个类型，方便管理
- value设置为不同的类型，方便服务器传递参数

设置提交按钮

- 将type设置为submit或者reset或者button
- value用来设置提交按钮的名字

## 属性和参数

输入框```<input type="" name="" value="" maxlength= placeholder="" checked/>```

- type参数有text，password，radio, checkbox, submit, reset, button, image, hidden, file
  - text：以明文作为文本
  - password：文本不显示
  - radio代表使用单选框
  - checkbox代表使用多选框
  - submit用于提交的按钮，默认将参数传输到本地
  - reset用于重置按钮
  - button代表普通按钮
  - image代表图片的提交按钮，使用src属性确定图片的路径
  - hidden代表隐藏的控件，用于服务器传输值
  - file代表文件上传，注意其对应的表单，method改成"post"，enctype改成"multipart/form-data"
- name用来标识属性，用于后台的交互，确定这个输入属于什么类型
  - 一般name是不同的
  - 对于单选框和多选框，需要使用名字来分组，确定是否为同一类型
- value代表输入的默认值
- maxlength代表能输入的最多的字符
- placeholder代表提示的信息，输入时自动清空
- checked用于单选框和多选框，代表默认勾选，写上就代表默认勾选

下拉列表```<select name="" size="3" multiple></select>```

- 代表可以观察到的选项个数
- multiple写上了就代表可以在下拉列表中选择多项
- name用于传参

- 可以选择的项```<option value="" selected></option>```
  - value用于服务器传递的值
  - selected代表默认选项

文本域```<textarea name="" placeholder="text" rows="10" cols="100"></textarea>```

- 只需要在文本域内输入内容即为指定默认值
- rows指定框能装载多少行
- cols指定一个行能装载多少个文字
- placeholder显示提示信息
- name表示传输的值

表单```<form action="" method="post" name="" enctype=""></form>```

- action
  - 默认提交到当前页面
  - 指定了action的值浏览器就会提交参数到另外的页面上（可以提交到任意服务器可以处理的地方）
- method：代表提交的方法，参数有get和pose
  - get：提交时把参数放到链接的后面（密码暴露）
  - pose：将数据封装成一个包（http请求），不放到链接里面
  - 一般的，网页链接后面加上?的后面都是使用get的方式传输数据
- 使用name确定标签
- enctype控制编码的格式，两种格式
  - application/x-www-form-urlencoded：默认值
  - multipart/form-data：用于上传文件

## 注意事项

表单：给用户提供输入的信息

使用表格控制文本的输入格式（账号，密码）