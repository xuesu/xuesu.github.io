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
- 在函数和数据类型定义中, 接MPI_之后的第一个字母大写，其余全部为小写字母，即MPI_Xxxx_xxx形式
- 除MPI_WTIME和MPI_WTICK外，所有C 函数调用之后都将返回一个错误信息码
- MPI 的所有C 函数中的输出参数用的都是指针
##2.5 MPI数据类型
- MPI datatype			
	- C datatype	
- MPI_CHAR				
	- signed char	
- MPI_SHORT				
	- signed short int	
- MPI_INT				
	- signed int	
- MPI_LONG				
	- signed long int	
- MPI_UNSIGNED_CHAR		
	- unsigned char	
- MPI_UNSIGNED_SHORT		
	- unsigned short int	
- MPI_UNSIGNED_INT		
	- unsigned int	
- MPI_UNSIGNED_LONG		
	- unsigned long int	
- MPI_FLOAT				
	- float	
- MPI_DOUBLE			
	- double	
- MPI_LONG_DOUBLE		
	- long double	
##2.7 编译运行
- mpiexec  – n 2 d:\mpijob\cpi.exe 
	- 在当前节点上启动两个进程
	- 多个进程使用同一个标准输出。
	- 只有一个进程能得到标准输入。


