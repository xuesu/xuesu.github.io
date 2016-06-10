#MPI

##通信子
在MPI中，通信子（communicator）指的是一组可以互相发送消息的进程集合。MPI\_Init的其中一个目的，是在用户启动程序时，定义由用户启动的所有进程所组成的通信子。这个通信子称为MPI\_COMM_WORLD
###MPI_INIT(&argc,&argv)
###MPI\_Comm\_rank(MPI\_COMM\_WORLD,&rank),MPI\_Comm\_size(MPI\_COMM\_WORLD,&size)
可以获取关于MPI\_COMM\_WORLD的信息

在MPI\_COMM\_WORLD中经常用参数size表示进程的数量，用参数rank来表示进程号。