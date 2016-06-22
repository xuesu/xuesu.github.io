##Chapter 9 Domain Model
###The most important OAA object, attribute, association
###Domain Model
1. illustrate meaningful conceptual classes in the problem domain
2. is a source of inspiration for design software objects

![](http://i.imgur.com/nx2DPJu.png)
###Avoid XXDatabase or function in Domain Model
##How to Create a Domain Model
1. Find the conceptual classes(List the candidate conceptural classes)
2. Draw them as classes in a UML class diagram
3. Add associations and attributes

##How to find Conceptual Classes
1. Reuse or modify existing models
2. Use a category list
3. Identify noun phrases

##Domain Modeling Guidelines
1. On Naming and Modeling things
	1. The Mapmaker Strategy or Use the Domain Vocabulary strategy
		1. Use the existing names in the territory
		2. exclude irrelevant features
		3. do not add things that are not there
2. A common mistake : represent something as an attribute when it should have been a concept
3. If X cant be thought as number or text, X is probably a conceptual class

##Description Classes
When there is a need to be a description about an item or service, independent or the current existence

Deleting instances of things they describe results in a loss of info that needs to be maintained

##The UML Association Notation
![](http://i.imgur.com/sFPeNat.png)

##Common Association List
![](http://i.imgur.com/kIw2s1z.png)
![](http://i.imgur.com/cZ7yyVE.png)