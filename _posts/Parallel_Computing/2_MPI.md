#MPI
Message Passing Interface

- 是一种标准或规范的代表，而不特指某一个对它的具体实现。迄今为止所有的并行计算机制造商都提供对MPI 的支持
- 最终目的是服务于进程间通信的目标
- 提供一个高效、可扩展、统一的并行编程环境
- 是一个库，不是一门语言，提供库函数/过程供C/FORTRAN 调用

目标

1. 较高的通信性能；
2. 较好的程序可移植性；
3. 强大的功能
##2.1 MPI进程
###MPI进程
MPI程序中一个独立参与通信的个体
###MPI进程组
MPI程序中由部分或全部进程构成的有序集合,每个进程都被赋予一个所在进程组中唯一的序号(rank)，用于在该组中标识该进程，称为进程号，取值从0开始，0，1，2......
##2.2 MPI Communicator
###MPI Communicator
MPI通信子,(MPI通信域,MPI通信器,)<b>包括进程组(Progress Group)和通信上下文(Communication Context),</b>同于描述通信进程之间的通信关系

MPI程序启动时自动建立通信器MPI\_COMM\_WORLD,包含程序中所有MPI进程
,之后用户可以根据自己的需要，建立其它的进程组

<b>进程间通信必须通过通信器进行</b>

####Communication Context
通信上下文：安全地区别不同的通信以免相互干扰，<font color='red'>通信上下文不是显式的对象，</font>只是作为通信域的一部分出现

##2.3 MPI消息
一个消息指进程之间的一次数据交换

####<font color='red'><b>消息构成</b></font>

- Message Buffer
	- buf
		- 起始地址
	- count
		- 个数
	- datatype
		- 数据类型
- Message Envelop
	- dest
		- 源/目标进程
	- tag
		- 消息标签
	- comm
		- 通信子
##2.4 MPI编程特征
- 在函数和数据类型定义中, 接MPI\_之后的第一个字母大写，其余全部为小写字母，即MPI\_Xxxx\_xxx形式
- 除MPI\_WTIME和MPI\_WTICK外，所有C 函数调用之后都将返回一个错误信息码
- MPI 的所有C 函数中的输出参数用的都是指针
##2.5 MPI数据类型
- MPI datatype			
	- C datatype	
- MPI\_CHAR				
	- signed char	
- MPI\_SHORT				
	- signed short int	
- MPI\_INT				
	- signed int	
- MPI\_LONG				
	- signed long int	
- MPI\_UNSIGNED\_CHAR		
	- unsigned char	
- MPI\_UNSIGNED\_SHORT		
	- unsigned short int	
- MPI\_UNSIGNED\_INT		
	- unsigned int	
- MPI\_UNSIGNED\_LONG		
	- unsigned long int	
- MPI\_FLOAT				
	- float	
- MPI\_DOUBLE			
	- double	
- MPI\_LONG\_DOUBLE		
	- long double	
##2.7 编译运行
- mpiexec  – n 2 d:\mpijob\cpi.exe 
	- 在当前节点上启动两个进程
	- 多个进程使用同一个标准输出。
	- 只有一个进程能得到标准输入。
- mpiexec – hosts 2  node1 3 node2  4 d:\mpijob\cpi
	- 在node1上启动3个进程，node2上启动4个进程。
##MPI常用接口
###初始化和结束
- int  MPI\_Init(int *argc, char ***argv)
	- 该函数初始化MPI 并行程序的执行环境，它必须在调用所有其它MPI 函数之前被调用，并且在一个MPI 程序中，只能被调用一次.
- int MPI\_Finalize(void)
	- 该函数清除MPI 环境的所有状态。即一但它被调用，所有MPI 函数都不能再调用，其中包括MPI\_INIT
###通信子
- int MPI\_Comm\_rank(MPI\_Comm comm, int *rank)
	- 该函数返回本进程在指定通信器中的进程号
- int MPI\_Comm\_size(MPI\_Comm comm, int *size)
	- 该函数返回指定通信器所包含的进程数
###发送数据
###接收数据
- MPI\_Recv(received\_request,100,MPI\_BYTE,MPI\_Any\_source,MPI\_Any\_tag,comm,&Status);


- 接收消息时返回的状态STATUS，在C 语言中是用结构定义的，其中包括MPI\_SOURCE，MPI\_TAG和MPI\_ERROR以及接收消息元素的个数，（用函数MPI\_GET\_COUNT来读取）
###其他
- double MPI\_Wtime(void)
	- 该函数返回当前的墙钟时间

- int MPI\_Get\_processor\_name(char *name, int *namelen)	
	- 该函数返回进程所在结点的主机名
##通信
###阻塞型检测
- int MPI\_Wait(MPI\_Request *request, MPI\_Status *status) 
	- 该函数是阻塞型的，它必须等待指定的通信请求完成后才能返回，与之相应的非阻塞型函数是MPI\_TEST。成功返回时，status中包含关于所完成的通信的消息，
	- 一个非阻塞的通信加上MPI\_Wait 等价于阻塞型通信。
###非阻塞型检测
- int MPI\_Test(MPI\_Request *request, int *flag, MPI\_Status *status)
	- 非阻塞型通信检测函数，不论通信是否完成都立刻返回，功能同MPI\_WAIT

##群集通信
1. 通信域中的所有进程必须调用群集通信函数。
2. 每个群集通信函数使用类似于点对点通信中的标准、阻塞的通信模式。
3. 一个群集通信操作是不是同步操作取决于实现。MPI要求用户负责保证他的代码无论实现是否同步都必须是正确的。
4. 所有参与群集操作的进程中，Count和Datatype必须是兼容的。
5. <b>消息信封由通信域和源/目标定义。</b>

###同步功能
int MPI\_Barrier(MPI\_Comm comm)	
###通信
####广播
- int MPI\_Bcast(void *buf, int count, MPI\_Datatype datatype, int root, MPI\_Comm comm)
	- root进程将自己buf中的内容广播发送到通信器内的所有进程（<b>包括它自身</b>）
####散发
- int MPI\_Scatter(void *sendbuf, int sendcount, MPI\_Datatype sendtype, void *recvbuf, int recvcount, MPI\_Datatype recvtype, int root, MPI\_Comm comm)
	- 根进程将这些数据块按进程的标识号依次分发给各个进程（包括root进程）
####收集
- int MPI\_Gather(void *sendbuf, int sendcount, MPI\_Datatype sendtype, void *recvbuf, int recvcount, MPI\_Datatype recvtype, int root, MPI\_Comm comm)	
	- 这n个消息按照进程的标识rank排序进行拼接，然后存放在Root进程的接收缓冲中。
###聚集
1. 首先是通信的功能，即消息根据要求发送到目标进程，目标进程也已经收到了各自需要的消息；
2. 然后是对消息的处理，即执行计算功能；
3. 最后把处理结果放入指定的接收缓冲区。

####规约Reduce
- int MPI\_Reduce(void *sendbuf, void *recvbuf, int count, MPI\_Datatype datatype, <b>MPI\_Op op</b>, int root, MPI\_Comm comm)	
- 普通归约：MPI\_REDUCE
	- 该函数将通信器内每个进程输入缓冲区（sendbuf）中的数据按给定的操作进行简单运算，并将其结果返回到根进程的输出缓冲区（recvbuf）中
- 归约运算可以使用MPI 预定义的运算操作，也可以使用户自己定义的运算操作
	- 自定义归约运算操作：MPI\_OP\_CREATE
	- 当自定义的运算不再需要时，可以将其释放，以释放其占用的系统资源
		- 释放自定义的归约操作：MPI\_OP\_FREE
![](http://i.imgur.com/k55Ce5T.png)
####扫描Scan
- int MPI\_Scan(void *sendbuf, void *recvbuf, int count, MPI\_Datatype datatype, MPI\_Op op, MPI\_Comm comm)
	- 可以把扫描操作看作是一种特殊的归约，即每一个进程都对排在它前面的进程进行归约操作




