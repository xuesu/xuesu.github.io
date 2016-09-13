#Cryptology-1
##Passive Attack & Active Attack
##History
1. 第一个阶段:1949年以前
	1. 古典加密
	2. 1883年Kerchoffs第一次明确提出了编码的原则：加密算法应建立在算法的公开不影响明文和密钥的安全。
1. 第二个阶段:1949年到1976年
	1. 标志:** Shannon 发表”Communication Theory of  Secrecy System”**
	1. 密码学进入了科学的轨道
	1. 主要技术: 单密钥的对称密钥加密算法
	2. 1967年David Kahn的《The Codebreakers》许多人了解了密码学
	3. 1971-73年IBM Watson实验室的Horst Feistel等几篇技术报告
		- 主要特点：数据的安全基于密钥而不是算法的保密 

1. 第三个阶段 :1976年以后
	1. 标志 : <b><font color = 'red' >Diffie,Hellman发表”New Directions in Cryptography”</font></b>
	1. 一种新的密码体制 : 公开密钥体制
	2. <b><font color = 'red' >Rivest,Shamir & Adleman RSA算法</font></b>
##Enigma (by Arthur Scherbius)
- 1925年，“谜”开始有系列生产
- 最后英国在“顺手牵羊”的行动中在德国潜艇上俘获“谜”的密码簿，破解了“谜”。
- 破译恩尼格玛而做出了重大贡献的三位杰出的波兰密码学家马里安·雷耶夫斯基(Marian Adam Rejewski)、杰尔兹·罗佐基(Jerzy Witold Różycki)和亨里克(Henryk Zygalski)
##Shannon

1. "A Mathematical Theory of Communication"(1948), This work focuses on the problem of how best to encode the information a sender wants to transmit. In this fundamental work he used tools in probability theory
2. 1949
	1. form basis of modern block ciphers 
	1. 	S-P nets are based on the two primitive cryptographic operations seen before: 
	1. 	substitution (S-box)
	1. 	permutation (P-box)
	1. 	provide confusion & diffusion of message & key

2. Shannon developed information entropy
3. "Prediction and Entropy of Printed English", proving that treating whitespace as the 27th letter of the alphabet actually lowers uncertainty in written language
4. **in 1949 ,"Communication Theory of Secrecy Systems"**,  in which he proved that all theoretically unbreakable ciphers must have the same requirements as the one-time pad. 

##Echelon
梯队系统是一个以美国为中心的情报收集分析网络的俗称。参与国家是英美防卫协定的五个签署国，英国、美国、加拿大、澳洲及新西兰。
它能够全球性地拦截以公众交换电话网络、卫星及微波通讯所传送的电话、传真，电子邮件和其他数位资讯，并监控其中的内容
##古典密码
1. 滚筒密码-移位
2. 凯撒密码-替代
	1. 可以穷举

##Symmetric cipher Model
![](http://i.imgur.com/Scbx2gY.png)
##Cryptosystem
- Quintuple (E, D, M, K, C)
- M set of plaintexts
- K set of keys
- C set of ciphertexts
- E set of encryption functions e: M * K -> C
- D set of decryption functions d: C * K -> M
##Language Redundancy and Cryptanalysis
- in English E is by far the most common letter 
- followed by T,R,N,I,O,A,S 
- other letters like Z,J,K,Q,X are fairly rare 
![](http://i.imgur.com/J4KEJhy.png)
##Block vs Stream Ciphers
- **block ciphers **process messages in blocks, each of which is then en/decrypted 
	- like a substitution on very big characters
	- 64-bits or more 
- **stream ciphers **process messages a bit or byte at a time when en/decrypting
	- many current ciphers are block ciphers
	- broader range of applications
	- stream ciphers RC4, A5/1, A5/2, A5/3
![](http://i.imgur.com/dDpQDN7.png)
