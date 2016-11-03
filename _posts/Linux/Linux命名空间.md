# Namespaces
isolation building blocks 统称为Namespaces

Linux 3.12内核支持六种Namespaces
1. UTS:hostname
2. IPC:进程间通信
3. PID:chroot进程树
4. NET:网络访问
5. NS:挂载点
6. User:将虚拟的userid映射到真实的userid

## Purpose
- to wrap a particular global system resource in an abstraction that makes it appear to the processes within the namespace that they have their own isolated instance of the global resource.
- to support the implementation of containers



The CLONE_NEW* identifiers listed in parentheses are the names of the constants used to identify namespace types when employing the namespace-related APIs 

# Mount Spaces(CLONE_NEWNS)
isolate the set of **filesystem mount points** seen by a group of processes. 

Thus, processes in different mount namespaces can have different views of the **filesystem hierarchy.**

the mount() and umount() system calls instead performed operations that affected **just the mount namespace associated with the calling process.**

# UTS(CLONE_NEWUTS)
LinuX Containers
1. 一种操作系统层次上的资源的虚拟化。
2. 容器有效地将由单个操作系统管理的资源划分到孤立的组中，以更好地在孤立的组之间平衡有冲突的资源使用需求。
3. 将不同应用的运行隔离

依赖linux运行的三种隔离机制
1. cgroups
2. chroot
3. namespaces(isolation building block)

- isolate two system identifiers—nodename and domainname—returned by the uname() system call; the names are set using the **sethostname() and setdomainname() system calls.**
- allows each container to **have its own hostname and NIS domain name.** This can be useful for initialization and configuration scripts that tailor their actions based on these names. 
- The term "UTS" derives from the name of the structure passed to the uname() system call: struct utsname. The name of that structure in turn derives from "UNIX Time-sharing System". 

## IPC (CLONE_NEWIPC)
- isolate certain **interprocess communication (IPC) resources**, namely, **System V IPC objects and (since Linux 2.6.30) POSIX message queues.** 
- IPC objects **are identified by mechanisms** other than filesystem pathnames. 
- Each IPC namespace has its own set of System V IPC identifiers and its own POSIX message queue filesystem. 

## PID(CLONE_NEWPID)
- isolate the **process ID number space**.
- containers can be migrated between hosts while keeping the same process IDs for the processes inside the container. 
- PID namespaces also allow each container to have its own init (PID 1), the **"ancestor of all processes"** that manages various system initialization tasks and reaps orphaned child processes when they terminate.
- a process has two PIDs: the PID inside the namespace, and the PID outside the namespace on the host system.

## Network(CLONE_NEWNET)
- provide isolation of the system resources associated with networking. 
- Thus, each network namespace has its own network devices, IP addresses, IP routing tables, /proc/net directory, port numbers, and so on
- each container can have **its own (virtual) network device and its own applications that bind to the per-namespace port number space**; suitable routing rules in the host system can direct network packets to the network device associated with a specific container. 

## User(CLONE_NEWUSER)
- isolate the user and group ID number spaces.
- a process can have a normal unprivileged user ID outside a user namespace while at the same time having a user ID of 0 inside the namespace. This means that the process **has full root privileges for operations inside the user namespace**, but is **unprivileged for operations outside the namespace.** 