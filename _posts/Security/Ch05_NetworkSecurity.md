#Chapter06_NetworkSecurity
##History of Denial of Service Attacks
1. Early 1990s:  Individual Attacks. First DoS Tools
1. Late 1990s:  Botnets, First DDoS Tools
1. Feb 2000:  First Large-Scale DDoS Attack
1. CNN, Yahoo, E*Trade, eBay, Amazon.com, Buy.com
1. 2004:  DDoS for hire and Extortion
1. 2007:  DDoS against Estonia
1. 2008:  DDoS against political dissident groups
1. 2008:  DDoS against Republic of Georgia during military conflict with Russia
##DoS Attacks
1. Spaming(垃圾邮件) & e-mail bomb
1. Ping of Death(ICMP)
	- 防御方法
		1. Block echo requests to broadcast networks
		1. Ban the IP of the attacker
		1. Filtering echo requests / Firewall
	- 用伪装的IP进行ping攻击
		- Smurf/Fraggle Attack
			- Use intermediate networks as amplification points
			- ![](http://i.imgur.com/v7puxwY.png)
			- Measure
				- Change firewall settings
				- Change router settings to not forward to broadcast IP addresses

1. <font color='red'>TCP SYN Flood DoS Attacks
	1. Attacker sends a SYN request and never responds to the SYN-ACK request
		1. Final ACK vs. IP spoofing
	1. Results in “half-open connection”
	1. Server resources consumed by these connections
		1. Timeout
	1. Allows no new connections</font>

1. Buffer Overflow
	-  Attempts to put more data, which would be long input strings, into the buffer than it can hold
	-  Code red, slapper and slammer are attacks that took advantage of buffer overflows
##Access Attacks 访问权限的获取
1. Eavesdropping
1. Interception 拦截窃听
1. Spoofing
	1. IP Spoofing 
		1. Remote machine acts as a node on the local network to find vulnerabilities with your servers, and installs a backdoor program or Trojan horse to gain control over network resources
		1. Pharming: **DNS Hijacking**
	2. Interface Spoofing
1. Password Guessing Attacks
	1. Brute Force Attack
	2. Dictionary Attack

1. Man-in-the-Middle Attacks
	- placing a piece of software between a server and user that they are aware of
	- Software intercepts data and then send the information to the server as if nothing is wrong

1. Social Engineering
