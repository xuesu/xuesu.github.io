#Network Security and Management 
##安全战略
1. 美国
	1. 网络安全战略计划CNAP
	1. 2001年10月4日 小布什 未经许可的国内监视项目
	2. 2001年10月26日 爱国者宣言
	3. 2005年11月16日 纽约时报披露国内监视项目
	1. 华为中兴事件:
		1. 2011年11月 对中国通讯公司的安全调查
		2. 2012年10月8日 认定华为中兴威胁国家安全
2. 中国
	1. 中央网络安全和信息化领导小组(习近平,李克强,刘云山)
##Science of Security
###Organizers
- David Evans, University of Virginia 
- Karl Levitt, National Science Foundation
- Brad Martin, National Security Agency
- James Silk, Institute for Defense Analyses 
###Defining Security
The security of a system, application, or protocol is always relative to

- A set of desired properties
- An adversary with specific capabilities

###Security Goals
####CIA
#####Confidentially
the avoidance of the unauthorized disclosure of information. 
######Tools
- Encryption
- Access Control
- Authentication
	- the determination of the identity or role that someone has. 
		- something the person has (like a smart card or a radio key fob storing secret keys),
		- something the person knows (like a password), 
		- something the person is (like a human with a fingerprint). 
- Authorization
	- the determination if a person or system is allowed access to resources, based on an access control policy. 
- Physical Security
	- the establishment of physical barriers to limit access to protected computational resources. 
#####Integrity
the property that information has not be altered in an unauthorized way.

######Tools
1. Backups
2. Checksums
3. Data correcting codes
#####Availability
the property that information is accessible and modifiable in a timely fashion by those authorized to do so.
######Tools
1. Physical protection
2. Computational redundancies
####AAA
- Assurance
- Authenticity
- Anonymity
#####Assurance
how trust is provided and managed in computer systems.
######Tools
- Policies
	- which specify behavioral expectations that people or systems have for themselves and others. 
- Permissions
	- which describe the behaviors that are allowed by the agents that interact with a person or system. 
- Protections
	- which describe mechanisms put in place to enforce permissions and polices.

#####Authenticity
the ability to determine that statements, policies, and permissions issued by persons or systems are genuine.

######Primary Tool
1. digital signatures
#####Anomynity
the property that certain records or transactions not to be attributable to any individual.
######Tools
- Aggregation
	- the combining of data from many individuals so that disclosed sums or averages cannot be tied to any individual. 
- Mixing
	- the intertwining of transactions, information, or communications in a way that cannot be traced to any individual. 
- Proxies
	- trusted agents that are willing to engage in actions for an individual in a way that cannot be traced back to that person. 
- Pseudonyms
	- fictional identities that can fill in for real identities in communications and transactions, but are otherwise known only to a trusted entity. 
##Threats and Attacks
###eavesdropping 窃听
the interception of information intended for someone else during its transmission over a communication channel.
###Alteration 修改
unauthorized modification of information. 
###Denial-of-service
the interruption or degradation of a data service or information access. 

- SPAM
- Email Bomber
###Masquerading 伪装
the fabrication of information that is purported to be from someone who is not actually the author.
###Repudiation 否认(接收)
the denial of a commitment or data receipt. 

This involves an attempt to back out of a contract or a protocol that requires the different parties to provide receipts acknowledging that data has been received.
###Correlation(相关) and traceback(追踪)
the integration of multiple data sources and information flows to determine the source of a particular data stream or piece of information.
##The ten Security Principles
[http://www.cs.arizona.edu/~collberg/Teaching/466-566/2012/Handouts/Handout-2.pdf](http://www.cs.arizona.edu/~collberg/Teaching/466-566/2012/Handouts/Handout-2.pdf)

1. economy of mechanism 架构经济,简单,尽可能小
	1. Keep the design and implementation as simple and small as possible.
2. fail-safe defaults 默认安全机制保守
	1. The default security configuration should be conservative
3. complete mediation 定时使用安全框架检查资源
	1. Every time a resource is accessed, the access should be checked against a protection scheme.
4. open design 架构公开
	1. The security architecture and design of a system should be made publically available.
	2. Security should rely only on keeping cryptographic keys secret. 
	3. is the opposite of <b>security by obscurity</b>
5. separation of priviledge 权限分离
	1. multiple conditions should be required to achieve access to restricted resources or have a program perform some action.
6. Least priviledge 权限最小化
	1. Each program and user of a computer system should operate with the bare minimum privileges necessary to function properly.
7. Least common mechanism 公共资源最小化
	1. mechanisms. allowing resources to be shared by more than one user should be minimized
8. Psychological acceptability 可被用户接受
	1. that user interfaces should be well designed and intuitive, and all security-related settings should adhere to what an ordinary user might expect.
9. Work factor 根据攻击者可能具有的资源设计绕过安全机制的代价
	1. the cost of circumventing (绕过) a security mechanism should be compared with the resources of an attacker when designing a security scheme. 
10. Compromise recording 记录被攻击的细节
	1. sometimes it is more desirable to record the details of an intrusion than to adopt more sophisticated measures to prevent it. 
