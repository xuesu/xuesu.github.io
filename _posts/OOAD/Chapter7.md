#Chapter 12: Requirements to Design
##Requirements to Design
1. iteratively do the right thing, do the thing right
2. provoke early change
3. didnt all that analysis and modeling take weeks to do

#Chapter 13 Logical Architecture & UML Package diagrams
##Goals
1. introduce a logical architecture using layers
2. illustrate the logical architecture using UML

![](http://i.imgur.com/W0kS1lW.png)

##what is the logical architecture and layers
1. the logical architecture is the large-scale of the software classes into packages, subsystems and layers
2. A layer is a very coarse-grained grouping of classes, packages or subsystems that has cohensive responsibility for a major respect of the system
3. typical layer in an OO system include
	1. user interface
	2. application logic and domain objects
	3. technical service
4. strict/relaxed layered architecture 

##What is software architecture
An architectrue is the set of significant decisions about the organization of a software system, the selection of the structure elements and their interfaces by which ther system is composed, together with their behavior as specified in the collaboration among those elements, the composition of these structural and behavioral elements into progressively larger subsystems- these elements and their interfaces, their collaborations and their composition

#Chapter 15 UML Interaction Diagram
Interaction Diagram

1. sequence Diagram
2. Communication Diagram

![](http://i.imgur.com/5CRCtSR.png)
![](http://i.imgur.com/MbChbry.png)
![](http://i.imgur.com/j03VR9F.png)
![](http://i.imgur.com/wBdAamO.png)

##单例模式
![](http://i.imgur.com/YfLEa4j.png)

##found message, execution specification bar, sychronous message
![](http://i.imgur.com/sEKbEV9.png)
##Reply 用虚线
##Messages to self
![](http://i.imgur.com/T4jw0QD.png)
##Object Creation & Destruction
![](http://i.imgur.com/9985Ii9.png)

##Common Frame Operator
1. alt
2. loop
3. opt
4. par
5. region
	1. only one thread can run

##Polymorphic Messages and Classes
![](http://i.imgur.com/jA3NK63.png)

##Asychronous Calls(stick arrow) synchronous call(filled arrow)

![](http://i.imgur.com/i1oGHfA.png)
![](http://i.imgur.com/msx0Eh5.png)