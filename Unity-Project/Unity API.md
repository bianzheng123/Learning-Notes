# Unity API

查看API文档

Help

unity manual

scripting reference

# 事件方法

Reset（）

- 只在添加脚本的时候才能触发
- 只在编译器中触发（发布后就不管了）

OnEnable（）

- setActive为true就调用

OnDisable（）

- setActive为false调用

OnLateUpdate（）

- Update之后调用

FixedUpdate（）

- 将一些运动放在里面，保证运动是平滑的

# Time

realTimeSinceStartup（）

在后台运行，游戏暂停时会一直增加

fixedTime（）

time（）

- 都是游戏运行的时间，如果在后台运行或者暂停就不算是计时了

timeSinceLevelLoad（）

- 切换场景重新开始计时

### 控制物体运行

cube.Translate(Vector3.forward * Time.deltaTime);

这样就能让物体平稳的运动

### 暂停游戏

Time.scale=0

这样乘上Time.deltaTime的物体都会暂停运动

Time.deltaTime的结果要乘上Time.scale

### 测试性能

Time.realtimeSinceStartup

用来测试哪个方法的性能更好

# GameObject

### 创建物体

Gameobject go = new GameObject("");

GameObject.Instantiate(prefab);

根据prefab创建，也可以根据另外一个游戏物体

GameObject.createPrimitive(PrimitiveType.Cube)

创建类似于cube，plane的原始图形

### 实例变量

activeInHierarchy

activeSelf

tag

当物体处于未激活状态，所有属性都能查找到，其update方法不再执行

### 静态方法

Find

根据名字查找

遍历所有的游戏物体，慎用

FindGameObjectsWithTag

FindWithTag

效率更高

### 实例方法

#### 游戏物体间消息发送和接收

物体都不需要用public修饰

BroadcastMessage(string methodname, paremeter...)

该物体以及孩子进行广播，不需要知道引用的对象，只要一个孩子里面有这个方法名，就执行广播

对于未激活的游戏物体，不会收到该广播消息

可以减少游戏物体之间的耦合性

拿到某个组件的引用比较复杂，就让广播消息的方法名传递过去，而不需要知道执行消息的人是谁

SendMessage(同上)

对单个的物体进行调用，而不对他的子物体进行调用

SendMessageUpwards(同上)

对当前物体及其父亲调用

# Object

### 静态方法

DontDestroyOnLoad(gameobject)

游戏物体不会在场景跳转中销毁

FindObjectOfType()

FindObjectsOfType()

不会查找未激活的游戏物体

### 实例变量

设置enabled用来禁用某个组件

# MonoBehavior

 Invoke（）

会先将需要调用的方法放到一个队列中，过一段时间再调用，所以，在方法被执行前IsInvoking（）都是为true，之后为false

Coroutine（）

isActiveAndEnabled（）

查看该组件是否激活

enabled

设置这个组件是否被激活

print（）

输出语句，只有在monobehavior才能调用

### 禁用组件

enabled=false