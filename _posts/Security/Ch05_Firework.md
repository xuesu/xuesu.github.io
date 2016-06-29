#Chapter 06 Filewalls
##Policy Actions
- Packets flowing through a firewall can have one of three outcomes:
	-  Accepted: permitted through the firewall
	-  Dropped: not allowed through with no indication of failure
	-  Rejected: not allowed through, accompanied by an attempt to inform the source that the packet was rejected
##Filewall Types
- packet filters (stateless)
	- If a packet matches the packet filter's set of rules, the packet filter will drop or accept it
	- Screening Router
- "stateful" filters
	- it maintains records of all connections passing through it and can determine if a packet is either the start of a new connection, a part of an existing connection, or is an invalid packet. 
- application layer
	- It works like a proxy it can “understand” certain applications and protocols. 
	- It may inspect the contents of the traffic, blocking what it views as inappropriate content (i.e. websites, viruses, vulnerabilities, ...)

##伪装信任主机/合法地址/电话拨号 绕过防火墙
##Demilitarized Zone DMZ 隔离区,控制区,非军事化区
那些需要从外部访问，但是需要一定保护措施的系统通常被设置在DMZ网络中，一般来讲，DMZ中的系统需要或者本身具有外部连通性。
##一体化威胁管理产品(Unified Threat Management Products, UTM）
One approach to reducing the administrative and performance burden is to replace all inline network products (firewall, IPS, IDS, VPN, antispam, antisypware, and so on) with a single device, a unified threat management (UTM) system, that integrates a variety of approaches to dealing with network-based attacks. A significant issue with a UTM device is performance, both throughput and latency, e.g. typical throughput losses for current commercial devices is 50%. 
Figure 9.6 is a typical UTM appliance architecture, in it note:
![](http://i.imgur.com/FRbLd4l.png)

1. inbound traffic is decrypted if necessary before its initial inspection. If the device functions as a VPN boundary node, then IPSec decryption would take place here.
2. an initial firewall module filters traffic, discarding packets that violate rules and/or passing packets that conform to rules set in the firewall policy.
3. then, a number of modules analyze individual packets and flows of packets at various protocols levels. A data analysis engine is responsible for keeping track of packet flows and coordinating the work of antivirus, IDS, and IPS engines.
4. the data analysis engine also reassembles multipacket payloads for content analysis by the antivirus engine and the Web filtering and antispam modules.
5. some incoming traffic may need to be re-encrypted to maintain internal security 
6. all detected threats are reported to the logging and reporting module, which is used to issue alerts for specified conditions and for forensic analysis.
7. the bandwidth-shaping module can use various priority and quality of service (QoS) algorithms to optimize performance.
#IDS
- assume intruder behavior differs from legitimate users
	- expect overlap as shown
	- observe deviations, from past history
- problems of:
	- false positives
	- false negatives
	- must compromise

##Type
基于主机or网络或混合
###Host-based IDS
specialized software to monitor system activity to detect suspicious behavior

检测内容： 系统调用、端口调用、系统日志、安全审记、应用日志

###Network-based IDS
1. Monitors traffic at selected points on the network
	1. Real time; packet-by-packet
![](http://i.imgur.com/lvgiczj.png)
##IDS detection Model
###<font color = 'red'>Misuse detection/signature detection</font>
- 基于知识的检测也称为误用检测，误用检测对检测的系统活动进行分析，试图发现那些与预定义好了的入侵特征相匹配的事件和事件集。


- 与入侵相对应的模式被称为特征，所以误用检测也被称为基于特征的检测。在目前的误用检测产品中，最常见的实现形式是将每一个入侵事件行为定义为一个特征描述，所有入侵行为特征描述就组成一个特征库。


- 误用检测系统通过对事件进行分析，提取出事件的特征模式，并与特征库进行匹配，由匹配结果来判断是否有入侵行为发生。


- 规则匹配是最常见的误用检测手段，目前也有比较复杂的误用检测技术，包括基于状态的分析技术和状态转换技术，都在一定程度上对简单的规则匹配技术进行了改进和提高。


- 误用检测技术的优点有：能准确迅速的检测到入侵模式库里已经定义好的入侵模式，而不会产生太多的误报；检测结果清晰明朗，容易对入侵事件有准确的定位；类似于杀毒软件的工作模式，便于升级维护。


- 存在的主要不足之处包括：对入侵模式库的依赖性很强，只能检测到已知的入侵模式，对新型入侵无能为力，容易产生漏报；入侵模式库的完备性难以保证，存在难于管理以及搜索的效率问题。
###<font color='red'>anomaly detection</font>
- 基于行为的检测也称为异常检测，异常检测技术基于用户行为和进程行为都有较大程度的稳定性这样一个前提。如果建立了用户行为和进程行为的正常模式，当出现较大的偏差异常时，则可以认为有恶意的入侵行为发生。


- 异常检测的关键问题是正常模式的建立以及对偏差的检测和判定，


- 在实现技术上，异常检测系统首先收集一段时间正常操作活动的历史数据，建立起代表用户、主机、网络连接的正常行为轮廓，然后收集事件数据并使用不同的方法来判断所检测的事件活动是否偏离了正常行为轮廓。


- 异常检测技术是目前入侵检测技术研究的热点领域，其所能达到的对未知入侵行为的检测能力令人神往，虽然目前还不能准确的做到这一点，但有一些研究至少可以表明这一点是能够做到的。
- 在异常检测领域主要的方法有：统计方法、机器学习方法、数据挖掘方法、聚类方法等。


- 异常检测技术的优点有：不依赖于具体的入侵知识，而是基于行为，可以检测到新型的入侵方式；不存在入侵模式库，避免了繁琐费时的搜索匹配工作，效率较高。


- 存在的主要不足之处：系统、用户、网络行为的复杂性导致正常模式的建立较为困难；统计方法的应用要有一定的前提；异常行为的判断很难做到准确，误报率较高。
###Hybrid
目前商业化的入侵检测产品大都是将误用检测技术和异常检测技术结合起来，以误用检测模块作为主体，异常检测模块作为有益的补充。


