#Chapter 16 UML Class Diagram
![](http://i.imgur.com/dcsk6Ha.png)
![](http://i.imgur.com/pY3q6bW.png)
![](http://i.imgur.com/mioAqcU.png)
![](http://i.imgur.com/ov8nWXE.png)
![](http://i.imgur.com/QT7jiQb.png)
#Chapter 17 GRASP Design Objects with Responsiblity
- What methods belong to where
- How the objects should interact

##Responsibilities and RDD
RDD: Responsibility-Driven Design

##GRASP
General Responsibility Assignment Software Patthern

describe fundamental principles of object design and responsibility assignment, expressed as patterns

##GRASP patterns
1. Information Experts
2. Creator
3. Controller
4. High Cohesion
5. Low Coupling
6. Polymorphism
7. Indirection
8. Pure Fabrication
9. Protected Variations

##创建者：谁创建了A？
解决方案：（有一个为真即可）
	1、B“包含”或组成聚集了A
	2、B记录A
	3、B紧密地使用A
	4、B具有A的初始化数据
##信息专家：如果给定键值，谁知道Square对象的信息？
解决方案：把职责分配给具有完成该职责所需信息的那个类
##低耦合：为什么是Board而不是Dog？如何减少变化产生的影响？
解决方案：分配职责以使耦合保持在较低的水平。用该原则对可选方案进行评估
##控制器：在UI层之上首先接受和协调系统操作的对象是什么？
解决方案：把职责分配给能代表下列选择之一的对象：
		1、代表全部“系统”、“根对象”、运行软件的设备或主要的子系统
		2、代表发生系统操作的用例场景（用例或会话）
##高内聚：怎样使对象保持有内聚、可理解和可管理，同时具有支持低耦合的附加作用？
解决方案：职责分配应保持高内聚，依此来评估备选方案
