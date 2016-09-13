#Chapter 9: Domain Model
![](http://i.imgur.com/MVdpd5s.png)
##Focus on DataType Attribute in the domain Model
1. The attribute should be primitive datatype
2. the attributes normally should not be a complex domain concept

![](http://i.imgur.com/wL08LBS.png)
###When to Define New DataType Classes
1. it is composed of separate sections
2. there are operations usually associated with it, such as parsing or validation
3. has other attributes
4. a quantity with a unit
5. an abstraction of one or more types with some of these qualities

#Chapter 10: System Sequence Diagram
System Sequence Diagram(SSD) is used to illustrate input and output events related to the system under discussion

is used to describe a particular scenario

![](http://i.imgur.com/Ux2wFlw.png)
![](http://i.imgur.com/ZTd9nHX.png)

#Chapter 11 Operation Contracts
Operation Contracts describe system behavior in terms of system changes to objects in the domain model, after a system operation is executed

the prime inputs to the contracts are the system operations identified SSD, the domain model, and domain insights from experts

![](http://i.imgur.com/EzWPiht.png)
the sections

1. operations
	1. name of operation
	2. parameters
2. cross reference
	1. use cases this operation can occur within
3. preconditions
4. postconditions

##Postconditions
1. instances create or be deleted
2. associations formed or broken
3. attribute changed

##When Are Contracts Useful
only where the details and complexity of required state changes are awkward to capture in use case, in UP, it is less effective

##How to create and write Contracts
1. identify system operations from SSDs
2. For System operations that are complex or which are not clear in the use case, construct a contract
3. when instance creation and deletion, attribute modification, associations formed and broken, describe the change in postcondition

