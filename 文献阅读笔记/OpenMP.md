+ 归约子句
```c
global_result = 0.0;
#pragma omp parallel num_threads(thread_count)\
  reduction(+: global_result)
global_result += Local_trap(double a, double b, int n);
```
    代码明确了global_result是一个归约变量，加号（“+”）指示归约操作是加法。OpenMP为每个线程有效地创建了一个私有变量，运行时系统在这个私有变量中存储每个线程的结果。OpenMP也创建了一个临界区，并且在这个临界区中，将存储在私有变量中的值相加。因此，对Local_trap的调用能够执行。
    reduction子句的语法是
```c
reduction(<operator>:<variable list>)
```
    当一个变量被包含在一个reduction子句中时，变量本身是共享的。然而，线程组中的每个线程都创建自己的私有变量。在parallel块里，每当一个线程执行涉及这个变量的语句时，它使用的其实是私有变量。当parallel块结束后，私有变量被整合到一个共享变量中。
+ 多个线程试图访问一个共享资源，并且至少其中一个访问是更新该共享资源，这可能导致错误。如引起竞争的代码global_result+=my_result，需要一些机制来确保一次只有一个线程执行。在OpenMP中，使用critical指令：
```c
#pragma omp critical
global_result += my_result
```
+ parallel for指令生成一组线程来执行后面的结构化代码块，必须是for循环
OpenMP只会并行化for循环，不会并行化while或do-while。OpenMP只能并行化那些可以确定迭代次数的for循环。例如，无限循环
```c
for(;;){
  ...
}
```
不能并行化。类似地
```c
for (size_t i = 0; i < n; i++) {
  if(...) break;
}
```
也不能并行化，因为迭代的次数不能只从for语句中来决定。这个for循环也不是一个结构化块，因为break提供了另一个从循环退出的出口。
+ 为了对线程进行调度，可以添加一个schedule子句到parallel for指令中：
```c
sum = 0.0;
#pragma omp parallel for num_threads(thread_count)\
 reduction(+:sum) schedule(static,1)
 for (size_t i = 0; i < n; i++) {
   sum += f(i);
 }

```
一般而言，schedule子句有如下形式：
```c
schedule(<type>[,<chunksize>])
