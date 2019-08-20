# DOM

DOM: Document Object Model，用于建立HTML/CSS和JavaScript之间的连接

DOM nodes

- document
- Element nodes
- attribute nodes
- text nodes

## API

读取标签

- `getElementById()`这个很快，查找哈希表即可，复杂度O(1)

- `querySelector`获取一个标记（搜索的第一个）

- `querySelectorAll`返回一个数组

- `querySelector`和`querySelectorAll`获取标签方式
  - tag的的名字（div）
  - id（记得加上#）
  - class属性（记得值前面加上.）
  - 通过属性的名字获取（记得加上'[这里填attribute，也可以加上值进行限定]'）

通过上述语句的返回值接受其信息

标签关键属性：

- `innerText`内部的标签，只读

- `childnodes`包括自己的子节点

- `children`不包括自己
- `nextElementSibling`
- `previousElementSibling`
- `textContent`设置其文本内容
- `innerHTML`同时设置标签和文本的内容

# jQuery

`document.createElement`里面写标签名字，返回的是其引用

`object.appendChild(elementInstance)`在某个节点上添加新的节点

`object.parentElement.removeChild(object)`用来移除自己，由于这个是树形结构，所以需要调用父节点来移除自己，不能自己移除自己

# 事件

响应用户的动作

对按钮添加class属性，通过querySelector()找到，使用object.addEventListener('click',onClick,false)方法添加

## 参数

object.addEventListener('string',method,false)

'string'可用的参数有三个：mouseover, click, mouseout

- mouseover指鼠标移动到按钮的区域
- click指鼠标按下按钮
- mouseout指鼠标移出区域

