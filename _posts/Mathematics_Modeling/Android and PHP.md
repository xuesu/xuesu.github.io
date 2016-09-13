<center>
#Andriod和PHP开发最佳实践
</center>
##1.准备篇
###1.2 为何选择Android和PHP
1. LAMP,Nginx + PHP fastCGI
###1.3
1. Android docs/reference/packages.html
2. PHP 文档 http://www.php.net/manual/
3. 官方拓展库 http://pecl.php.net/packages.php
##
###2.1 Android背景知识
1. 基于linux平台
###2.2 Android系统框架
![](http://i.imgur.com/jawxMci.png)

1. Applications
2. Application Framework
3. Libraries
4. Android Runtime

![](http://i.imgur.com/qiitZDD.png)

![](http://i.imgur.com/1GXC8uX.png)

####Android Runtime
1. Android基本符合linux内核标准
2. 文件系统:YAFFS2
2. IPC Binder通过Service Manager管理系统中的服务,各进程通过访问Binder访问同一块共享内存,以达到数据共享的目的.
3. LMK(Low Memory Killer)关闭最低重要级别的进程,Ashmem(Anonymouse Shared Memory)
4. 没有休眠待机功能,可以通过RPC调用,电池状态改变和电源设置判断调整电源管理策略.
###2.3 Android应用框架
1. 要点
	1. Activity
	2. Intent
	3. View
	4. Task
2. Activity
	1. ![](http://i.imgur.com/GhrJBTZ.png)
	2. Activity:界面控制器,类似于网页
	3. Android系统内部有专门的Activity堆栈空间,用于存储多个Activity的运行状态
	4. 系统保证某一时刻只有最顶端的Activity处于前端活动foreground状态
	5. 启动并进入活动状态OnCreate->onStart->onResume
	6. 退居后台onPause->onStop
	7. 重新回到活动状态onRestart->onStart->onResume
	8. 销毁onPause->onStop->onDestroy
	9. 所有Activity必须在项目基础配置文件AndroidManifest.xml中声明,否则可能抛出ActivityNotFoundException异常
3. 消息Intent
	1. 一个对象,包含构成消息的内容和属性
		1.	ComponentName,用于指定目标组件,可以送过setComponent,setClass,setClassName设置
		2.	Action,定义了各种动作常量(字符串常量)setAction方法
			1.	ACTION_MAIN表示应用入口初始化动作
			2.	ACTION_EDIT 常见的编辑动作
			3.	ACTION_CALL 初始化电话模块动作
		3. Data,setData,SetType
			1. 不同动作对应不同数据类型
			2. 数据类型可以从URI格式中获取
		4. Category,addCategory
			1.  不同动作由不同类别的Activity组件处理,一个Intent对象可以包含多种类型属性
		5. Extras
			1. 自定义额外附加信息,以键值对方式存储,
			2. get/putExtra
		6. Flags
			1. 用于指示Android系统如何启动Activity以及启动之后如何处理
	2. 使用方式
		1. 显式消息 Explicit Intent
			1. 
		2. 隐式消息 Implicit Intent