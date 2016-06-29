#Ch03_Public_Key_Cryptography_and_RSA
##Diffie-Hellman 密钥交换算法
- 仅限于密钥交换
- all users agree on global parameters:
	- large prime integer or polynomial q
	- g being a primitive root mod q (本原根,g及g的幂次%p可以生成0-p-1,即所有余数)
- each user (eg. A) generates their key
	- chooses a secret key (number): xA < q 
	- compute their public key: yA = g^{xA} mod q
-  each user** makes public that key yA**
-  KAB = g^{xA*xB} mod q

	= yA^{xB} mod q  (which B can compute) 

	= yB^{xA} mod q  (which A can compute) 
###中间人攻击
![](http://i.imgur.com/Xt5Xjbi.png)

##RSA
Rivest,Shamir,Adleman

A Method for obtaining Digital signatures and Public-key Cryptosystem

###Process
1. By Rivest, Shamir, and Adleman (MIT)
1. RSA is the gold standard in public key crypto
1. Let p and q be two large prime numbers
1. Let N = pq be the modulus
1. Choose e relatively prime to (p-1)(q-1)
1. Find d such that ed = 1 mod (p-1)(q-1)
1. Public key is (N,e)
1. Private key is d
1. To encrypt M we compute
1. C = M^e mod N 
1. To decrypt ciphertext C compute
1. M = C^d mod N 

