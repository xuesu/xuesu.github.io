#Xpath,XLink & XPointer
-----
1. XPath:locate nodes and fragments
	- used both in XPointer,XSL,XML Schema,XQuery
2. XLink:a generalization of the HTML link concept
3. XPointer: an extension of XPath suited for linking
	- specifies connection bewteen Xpath expressions and URIs
4. XPath:
	- / root directory
	- /users/dave every dave in every users below the root
	- <b>.</b> the current directory
	- **..** the upper directory
	- **//** any elements
	- **[]** start from 1
	- **last()** [last()]
	- <b>*</b> wild card
	- **@attribute** chapter[not@num]
5. 