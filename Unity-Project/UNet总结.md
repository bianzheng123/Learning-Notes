# UNet总结

## 组件

Network ManagerHUD

- 控制显示网络连接的UI

Network Manager

- 用于连接网络
- 在空物体上创建这个组件
- 游戏内的物体不需要该组件
- Spawn Info
  - 代表生成的角色是在哪一个prefab

Network Identity

- 凡是涉及到网络的游戏物体，都要使用该组件
- 使得每一个客户端都有对应的生成的角色
- sever only：在服务器端创建该角色，客户端不显示
- Local Player Authority：如果客户端需要控制该角色，就将其勾上
  - 在服务器端中，修改服务器端的玩家可以实现同步，但是修改客户端的玩家不能实现同步

Network Transform

- 用来同步不同玩家的transform, Rigidbody组件
- Network Send Rate指同步速率，对于运动轨迹恒定的游戏物体，可以将同步速率设置为0，而玩家是不规则运动，所以同步速率要高一点
- 同步的方式是：localPlayer同步到其他的客户端
  - 客户端改变其他玩家的transform组件是不可取的

## API

OnStartLocalPlayer

- 这个方法只会在本地角色那里调用
- 需要对这个方法进行重写

```isLocalPlayer()```判断该组件是否由本地用户控制

Transform

- rotation是指相对于世界坐标系的旋转方向，是一个四元数
- 使用```gameobject.transform.forward```来表示一个游戏物体自身坐标系的向前的方向，而不是恒定的(1,0,0)

RIgidbody

- velocity用来设置速度，是一个向量

```NetworkServer.Spawn(gameobject);```

- 该游戏物体在sever端生成时，在客户端生成该游戏物体的副本

```[Command]```  表示客户端向服务端发送的命令,在服务端执行

```[ClientPrc]```  表示服务端向客户端发送的命令,在客户端执行

## 操作细节

测试

- build一个游戏，用来模拟多个服务器

玩家控制自己的角色

- 导入UnityEngine.Networking包
- 继承自NetworkBehaviour类
- 调用里面的isLocalPlayer()，判断是否为本地用户

设置子弹的方向

- 在枪的末尾设置一个空物体
- 获取这个空物体的transform组件
- 则子弹的出生位置就是这个空物体的位置，方向就是旋转的方向

使生成的游戏物体显示在sever中

- 生成的游戏物体添加network identity组件
- Network Manager的Registered Spawnable Prefabs添加会在游戏中生成的游戏物体

使方法在客户端调用，服务器端执行

- 在函数外部添加```[Command]```
- 注意这样的方法名前缀一定要加Cmd，用来标记

显示血条

- 使用slider创建一个血条
- 删除Handle Slide Area
- 将Fill拖到Background下面，并删除Fill Area
- 设置Fill锚点，按下alt键，并点击右下角，使得和父物体的大小同步
- 这样在Slider下面的value就可以实现完全覆盖

- Fill选择绿色，代表满血
- Background选择红色，代表空血

人物上方显示血条

- 将Canvas作为人物的子物体中
- Render Mode改成World Space
- 调整大小，将血条至于人物上方即可

使得画布一直面向照相机

- 添加脚本到Canvas下面
- 在update下面添加语句```transform.lookAt(Camera.main.transfrom)```

同步血量

- 当检测到子弹碰撞时，判断是否为服务器端，如果是，返回
- 需要同步的是currentHealth变量，将该变量前面加上一个特性```[SyncVar]```
- 同步血量时实时检测
  - 修改特性为```[SyncVar(hook="OnChangeHealth")]```
  - 只要这个变量的值发生了改变，就会调用OnChangeHealth方法
  - 然后重写OnChangeHealth方法即可，这样同一个事件，服务器端和客户端就会调用不同的方法
  - OnChangeHealth方法中只能写一个参数，就是检测到修改过后的值

使玩家重生

- Network Identity属性使得了本地客户端无法修改其他的客户端的玩家属性
- 对于重生的方法，添加```[ClientRpc]```特性使得客户端能调用该方法
- 由于客户端会对每一个player进行检测，所以需要进行是否为LocalPlayer的判断
- 对于这类方法一定要以Rpc开头

设置角色的不同出生位置

- 创建空物体，设置其位置，作为随机出生点
- 对这个物体添加Network StartPosition组件
- 在NetworkManager -> Spawn Info -> Player Spawn Method改成Round Robin

## 注意要点

如果脚本继承自monobehaviour，则对于本地玩家会控制其他玩家的角色

使用```GetComponent<MeshRenderer>().material.color```设置游戏物体的颜色

敌人，玩家一般都是放在sever端进行生成

不论什么方式，客户端都不会执行方法，都是在客户端调用方法，服务器端执行方法

1. 对于客户端控制的人物发射子弹这种行为，子弹不是在客户端生成的，而是客户端调用方法，在服务器端执行，生成子弹
2. 服务器端生成的子弹需要在客户端生成副本，在客户端上才能看见

对于碰撞检测，只会在服务器端做，然后同步到每一个客户端

- 服务器端的子弹被销毁，则客户端的子弹一定会被销毁
- 客户端的子弹被销毁，则服务器端的子弹不一定被销毁
- 这样就会导致扣血不同步的问题

只要用到了判断是否为服务器端，就要继承自NetworkBehaviour

和人物角色无关的，比方说子弹，都是在服务器端生成的

对于和人物角色有关的，比方说角色重生，则是在客户端进行响应（Network Identity限制了）

## 总结

对于人物角色的生成

- 由于是开局生成的人物模型，所以在Network Manager的Player Prefabs下面将Player拖拽进去
  - 自动生成玩家，auto create player勾选

- 使用network identity显示
- 需要在多个端上同步角色的移动，所以添加Network Transform
- 客户端需要控制该角色，所以Local Player Authority勾上

对于子弹的生成

- 子弹属于游戏物体的一种，在按空格后生成，所以Network Manager中Registered spawn prefab添加子弹

- 客户端不需要控制子弹飞行，故只需创建Network Identity即可
- client需要看到子弹，所以使用NetworkServer.spawn(gameobject)对每一个client创建一个子物体
- 子弹需要在client上看到飞行的模式，所以添加Network Transform
  - 子弹飞行速度恒定，故同步的速率可以为0

对于角色被子弹击中

- 为了正确同步，所有的碰撞检测都是在server内进行的
- 当角色被击中时，server会将改变的数值health发送到客户端，客户端通过指定的方法进行同步
- 由于检测子弹只在服务器中运行该方法，所以说没有health没有进行血量上的同步，就需要引入特性达到血量同步的目的

角色重生

- 判断掉血是在server中进行
- 重生需要控制其他角色的引用，但是Network Identity决定了不能在服务器端调用客户端的角色
- 就需要添加特性使得重生的方法在客户端直接调用

销毁敌人

- TakeDamage只在服务器运行，所以销毁方法也只在服务器中运行
- 运行时，自动同步的东西有：物体是否销毁
- 所以说不需要添加额外的代码即可时的客户端出现销毁画面

Command，ClientRpc，SyncVar对比

- Command是客户端发送到服务器端进行处理的方法
- ClientRpc是服务端发送到客户端进行执行的方法
- SyncVar是客户端上的数值有改变，并同步到服务端上的