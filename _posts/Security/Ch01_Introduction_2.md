##Access Control
###Question
1. Which users can read/write which files?
1. Are my files really safe?
1. What does it mean to be root?
1. What do we really want to control?
###Elements
1. Users and groups
1. Authentication
1. Passwords
1. File protection
1. Access control lists
###Access Control Matrices
A table that defines permissions. 

1. row:a user, group, or system that can perform actions. 
1. column:a file, directory, document, device, resource, or any other entity for which we want to define access rights. 
1. cell:the access rights for the associated combination of subject and object. 
	1. Access rights can include actions such as reading, writing, copying, executing, deleting, and annotating. 
	1. An empty cell means that no access rights are granted.


![](http://i.imgur.com/z2SFHfL.png)

###Access Control Lists
![](http://i.imgur.com/JqLaVsu.png)
###Capabilities
![](http://i.imgur.com/5wZKXmI.png)
###Role-based Access Control
Define roles and then specify access control rights for these roles, rather than for subjects directly.
##Encryption and Decryption
	C = E(M)
	M = D(C)

###Cryptosystem
1. The set of possible plaintexts
1. The set of possible ciphertexts
1. The set of encryption keys
1. The set of decryption keys
1. The correspondence between encryption keys and decryption keys
1. The encryption algorithm to use
1. The decryption algorithm to use
####Caesar Cipher 移位密码
####Symmetric Cryptosystems
secret key is used for both encryption and decryption.
####Public-Key Cryptography
the sender uses the public key of the recipient to encrypt and the recipient uses its private key to decrypt. 
#####application:Digital Envelope
![](http://i.imgur.com/YH053pB.png)
#####application:Digital Signature
To sign a message, M, Alice just encrypts it with her private key, SA, creating C = ESA(M).

Anyone can decrypt this message using Alice’s public key, as M’ = DPA(C), and compare that to the message M. 
##Cryptographic Hash Functions
A checksum on a message, M, should be: One-way, Collision-resistant
###Message Authentication Codes
![](http://i.imgur.com/hHoXE5p.png)
###Certificate authority
digitally signs a binding between an identity and the public key for that identity.
##Password
###What is a strong password
1. UPPER/lower case characters
2. Special characters
3. Numbers

Odd character, Longer Password,
###Password Validity: Brute Force Test
##Social Engineering
1. Pretexting 借口:creating a story that convinces an administrator or operator into revealing secret information.
2. Baiting 诱饵:offering a kind of “gift” to get a user or agent to perform an insecure action.
3. Quid pro quo 交换物: offering an action or service and then expecting something in return.

