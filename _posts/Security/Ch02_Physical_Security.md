#Chapter 2 Physical Security
##Category
1. Physical Protections and Attacks
1. Locks and Safes
1. Authentication Technologies
1. Direct Attacks Against Computers
1. RFID security
##Physical Protections and Attacks
- Location protection 保护主机物理位置: the protection of the physical location where computer hardware resides, such as through the use of locks. 
- Physical intrusion detection 侵入主机所在位置: the detection of unauthorized access to the physical location where computer hardware resides.
- Hardware attacks 攻击硬件: methods that physically attack the hardware representations of information or computations, such as hard drives, network adapters, memory chips, and microprocessors.
- Eavesdropping 监听(硬件变化): attacks that monitor light, sound, radio, or other signals to detect communications or computations.
- Physical interface attacks 攻击物理接口: attacks that penetrate a system’s security by exploiting a weakness in its physical interface.
###Destructive   vs. Nondestructive  Entry
###Bypass : Side Channel Attacks
###Barcode 条形码
as two-dimensional patterns 二维码
####Authentication via Barcodes
however, barcodes provide convenience but not security. 
###Smart Cards
optionally with an on-board microprocessor

Smart card technology are extremely difficult to duplicate. 
###SIM Cards
subscriber identity module card

A SIM card is issued by a <b>network provider</b>. It maintains personal and contact information for a user and allows the user to authenticate to the cellular network of the provider.
###Passport
an embedded RFID 
###offensive:Wiretapping 窃听器
###offensive:Acoustic Emission
an attacker could use an audio  recording of a user typing on a keyboard to reconstruct what was typed. 
###offensive:Hardware keyloggers
###defensive:Faraday Cages
###Computer Forensics
obtaining evidence contained on an electronic medium to be used in legal proceedings
###ATM-3DES
automatic teller machine
####Attacks
1. Lebanese loop
2. Skimmer
3. Fake ATMs
##computer Forensics
![](http://i.imgur.com/55zSNJQ.png)

1. capture more volatile evidence first
2. Hidden Data in the Hard Drive Slack Space
	1. The logical end of the file (i.e., the end of the data actually in the file) and 
	2. The physical end of the file (i.e., the end of the last sector devoted to the file).
3. Create a Duplicate Image
###How to Hide Data?
1. Cryptography
1. Steganography 
	1. The process of hiding data inside other data (e.g. image files). 
1. Change file names and extensions
	1. E.g. rename a .doc file to a .tmp file
1. Hidden tracks
	1. most hard disks have # of tracks hidden (i.e. track 0)
	1. They can be used to hide/read data by using a hex editor
1. Deleted Files
	1. not truly deleted, merely marked for deletion. 
##Disk Wiping
- Simple erase
	- The data is still on the drive but the segment has been marked as available
	- Next time data is written to the drive it MAY overwrite the segment
- Destructive erase
	- First overwrites all data in the file with random data
	- Next marks the segment as available
	- It may be possible to find ghost images of what was previously on the disk surface
