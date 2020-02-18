# Spring_02

## ioc

spring需要知道所有的对象，还要知道对象是什么，需要干什么

然后spring就会把你想要的主动给你，同时把你交给需要你的地方

**所有的对象都被spring控制（控制反转）**

## di

依赖注入

将需要的东西注入到目标的需求

spring是在启动项目的时候实例化xxxService

### 使用xml指定注入

### 使用注解代替xml

推荐使用@Resource(name="userService")

## aop

面向切面编程

例子

- 使用filter解决servlet的乱码问题

连接点：目标对象中，所有**可以**增强的方法（filter可以覆盖到的方法）

切入点：目标对象中**已经**增强的方法（使用filter覆盖过的）

通知：增强的代码（filter的具体实现）

目标对象：被代理（增强）的对象（被filter覆盖的各个servlet）

织入：将通知应用到切入点的过程（将filter的代码嵌入到servlet执行流程的过程）

代理：将通知织入到目标对象之后形成的对象（将filter嵌入到servlet后形成的新对象）

切面：切入点+通知