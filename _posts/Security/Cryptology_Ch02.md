##Chapter 02 Cryptology
##无密钥体制
1. A将密文加密,发给B
2. B再将密文加密,发给A
3. A解密自己的密文,发回B
4. B解密自己的密文

特点:
1. 不需要交换秘钥
2. 未找到安全算子

##单钥/对称体制
###1949,Shannon
1. form basis of modern block ciphers 
1. S-P nets are based on the two primitive cryptographic operations seen before: 
1. substitution (S-box)
1. permutation (P-box)
1. provide confusion & diffusion of message & key
####S-box
Substitution
####P-box
Permutation
####Confusion 使密码和密文之间的联系复杂
makes relationship between ciphertext and key as complex as possible
####Diffusion 模糊明文统计结构 
issipates statistical structure of plaintext over bulk of ciphertext
##Feistel Cipher structure
1. data split in 2 halves, 
2. processed through a number of rounds which perform a substitution on left half using output of round function on right half & key, 
3. and a permutation which swaps halves, as listed previously.

![](http://i.imgur.com/nyqv8gr.png)
