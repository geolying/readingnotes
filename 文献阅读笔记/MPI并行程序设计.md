+
```c
/*test_mpi.c*/
#include "mpi.h"
#include <math.h>
#include <stdio.h>
int main(int argc, char *argv[]) {
  int myid, numprocs;
  int namelen;
  char processor_name[MPI_MAX_PROCESSOR_NAME];

  MPI_Init(&argc, &argv);
  MPI_Comm_rank(MPI_COMM_WORLD, &myid);
  MPI_Comm_size(MPI_COMM_WORLD, &numprocs);
  MPI_Get_processor_name(processor_name, &namelen);

  fprintf(stderr, "Hello world! Process %d of %d on %s\n", myid, numprocs,
          processor_name);
  MPI_Finalize();
  return 0;
}

```
```shell
mpicc -o test test_mpi.c
mpirun -np 50 ./test
```
+ MPI程序的一些惯例
所有MPI的名字都有前缀“MPI_”，不管是常量、变量还是过程或函数调用的名字。自己编写的程序不能出现任何以前缀“MPI_”开始的任何变量和函数。
C形式的MPI调用，以MPI_Aaa_aaa的形式。
+
```c
int MPI_Init(int *argc,char ***argv);//MPI初始化

int MPI_Finalize(void);//MPI结束

int MPI_Comm_rank(MPI_Comm comm,int *rank);//当前进程标识
/*******************************************************************************
  IN:   comm      该进程所在的通信域（句柄）
  OUT:  rank      调用进程在comm中的标识号
这一调用返回调用进程在给定的通信域中的进程标识号，有了这一标识号，不同的进程就可以将自身和其它的进程区别开来，实现各进程的并行和协作
*******************************************************************************/

int MPI_Comm_size(MPI_Comm comm,int *size);//通信域包含的进程数
/*******************************************************************************
  IN:   comm      通信域（句柄）
  OUT:  size      通信域comm内包含的进程数
这一调用返回给定的通信域中所包括的进程的个数，不同的进程通过这一调用得知在给定的通信域中一共有多少个进程在并行执行
*******************************************************************************/

int MPI_Send(void *buf,int count,MPI_Datatype datatype,int dest,int tag,MPI_Comm comm);//消息发送
/*******************************************************************************
  IN:   buf        发送缓冲区的起始地址（可选类型）
  IN:   count      将发送的数据的个数
  IN:   datatype   发送数据的数据类型（句柄）
  IN:   dest       目的进程标识号（整型）
  IN:   tag        消息标志（整型）
  IN:   comm       通信域（句柄）
该函数将发送缓冲区中的count个datatype数据类型的数据发送到目的进程，目的进程在通信域中的标识号是dest，本次发送的消息标志是tag，使用这一标志，就可以把本次发送的消息和本进程向同一目的的进程发送的其他消息区别开来。
该操作指定的发送缓冲区是由count个类型为datatype的连续数据空间组成，起始地址为buf。其中datatype数据类型可以是MPI的预定义类型，也可以是 用户自定义的类型。通过使用不同的数据类型调用MPI_Send，可以发送不同的数据类型。
*******************************************************************************/

int MPI_Recv(void *buf,int count,MPI_Datatype datatype,int source,int tag,MPI_Comm comm,MPI_Satus *satus)
/*******************************************************************************
  OUT:    buf           接收缓冲区的起始地址（可选数据类型）
  IN:     count         最多可接收的数据的个数（整型）
  IN:     datatype      接收数据的数据类型（句柄）
  IN:     source        接收数据的来源即发送数据的进程的进程标识号（整型）
  IN:     tag           消息标识，与相应的发送操作的表示相匹配相同（整型）
  IN:     comm          本进程和发送进程所在的通信域（句柄）
  OUT:    status        返回状态（状态类型）
MPI_Recv从指定的进程source接收消息，并且该消息的数据类型和消息标识和本接收进程指定的datatype和tag相一致，接收到的消息所包含的数据元素的个数最多不能超过count。
接收缓存区是由count个类型为datatype的连续元素空间组成，由datatype指定其类型，起始地址为buf。接收到消息的长度必须小于或等于接收缓冲区的长度。
*******************************************************************************/

int MPI_Bcast(void* buffer,int count,MPI_Datatype datatype,int root, MPI_Comm comm)
/*******************************************************************************
IN/OUT　   buffer　　  通信消息缓冲区的起始地址(可变)
　IN　　　 count　  　 通信消息缓冲区中的数据个数(整型)
　IN 　　　datatype 　通信消息缓冲区中的数据类型(句柄)
　IN　　　 root　  　　发送广播的根的序列号(整型)
　IN 　　　comm   　　通信子(句柄)
MPI_BCAST是从一个序列号为root的进程将一条消息广播发送到组内的所有进程,包括它本身在内.调用时组内所有成员都使用同一个comm和root,其结果是将根的通信消息缓冲区中的消息拷贝到其他所有进程中去
*******************************************************************************/
```
+ MPI消息包括信封和数据两个部分，信封指出了发送或接收消息的对象及相关信息，而数据是本消息将要传递的内容，信封和数据又分别包括三个部分，可以用一个三元组来表示：
信封：<源/目，标识，通信域>
数据：<起始地址，数据个数，数据类型>
```c
MPI_Send(void *buf,int count,MPI_Datatype datatype,int dest,int tag,MPI_Comm comm)
```
    前三个参数（buf,count,datatype）是消息数据，后三个参数（dest,tag,comm）是消息信封
```c
MPI_Recv(void *buf,int count,MPI_Datatype datatype,int source,int tag,MPI_Comm comm,MPI_Satus *satus)
```
    前三个参数（buf,count,datatype）是消息数据，后三个参数（source,tag,comm）是消息信封
+ MPI通信域包括两部分：进程组和通信上下文。进程组即所有参加通信的进程的集合，如果一共有N个进程参加通信，则进程的编号从0到N-1；通信上下文提供一个相对独立的通信区域，不同的消息在不同的上下文中进行传递，不同上下文的消息互不干涉，通信上下文可以将不同的通信区别开来。
一个预定义的通信域MPI_COMM_WORLD由MPI提供。MPI初始化后，便会产生这一描述子，它包含了初始化时可得的全部进程，进程是由它们在MPI_COMM_WORLD组中的进程号所标识。
用户可以在原有的通信域的基础上，定义新的通信域。通信域为库和通信模式提供一种重要的封装机制，它们允许各自模式有其自己的独立的通信域，和它们自己的进程计数方案。
+ 用MPI实现计时功能
```c
double MPI_Wtime(void)
```
    MPI_Wtime返回一个用浮点数表示的秒数，它表示从过去某一时刻到调用时刻所经历的时间。这样如果需要对特定的部分进行计时，一般采取的方式是：
```c
double starttime, endtime;
...
starttime = MPI_Wtime;
/*需计时部分*/
endtime = MPI_Wtime;
printf("That tooks %f seconds\n",endtime-starttime );
```
+ 捆绑发送和接收操作把发送一个消息到一个目的地和从另一个进程接收一个消息合并到一个调用中，源和目的地可以是相同的。捆绑发送接收操作虽然在语义上等同于一个发送操作和一个接收操作的结合，但是它可以有效地避免由于单独书写发送或接收操作时，由于次序的错误而造成的死锁。这是因为该操作由通信系统来实现，系统会优化通信次序，从而有效地避免不合理的通信次序，最大限度避免死锁的产生。(p55)
```c
int MPI_Sendrecv(void *sendbuf,int sendcount,MPI_Datatype sendtype,int dest,
int sendtag,void *recvbuf,int recvcount,MPI_Datatype recvtype,int source, int recvtag,MPI_Comm comm,MPI_Satus *status)
```
+ MPI共有四种通信模式，即标准通信模式(standard mode, MPI_Send)，缓存通信模式(buffered-mode,MPI_Bseng)，同步通信模式(synchronous-mode,MPI_Ssend)和就绪通信模式(ready-mode,MPI_Rsend)。
+ 程序设计中的错误
1）对status的错误声明
status是一个整数数组，而不是一个整数，在MPI_Recv调用中，一些返回信息保存在status中，由于一些编译器对它的检查不严格，这样在程序运行时，便经常出现写变量出界而产生不可预见的错误。
2）不要在MPI_Init前和MPI_Finalize后写可执行程序代码
这些位置MPI标准没有定义，执行会出现不可预料的结果
3）MPI_Send和MPI_Recv的不合理次序
可能造成系统内存空间缺失，形成死锁
4）数据类型不匹配
5）接收缓冲区溢出
接收缓冲区太小，但允许接收的数据容量却超过了接收缓冲区的大小。
