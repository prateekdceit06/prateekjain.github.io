---
layout: post
title:  "Parallelization of Borůvka's algorithm"
date:   2020-12-11 13:25:13 -0400
categories: parallel-computing graph-algorithm Borůvka-algorithm
background: style-2
description: At a Georgia Tech research program, the author parallelized Borůvka's algorithm for minimum spanning trees using Java Habanero. They compared multithreaded program performance across different thread and core counts, maximizing CPU utilization with concurrent thread execution, and leveraging the Thread class or Runnable interface.
---
During my research summer program at Georgia Tech, I implemented parallelization of Borůvka's algorithm to find the minimum spanning tree of an undirected graph. The idea was to implement a multithreaded program of Borůvka's algorithm using Java Habanero and compare its performance for the different number of threads and cores. Multithreading allows concurrent execution of two or more parts of a program for maximum utilization of CPU. Each part of such a program is called a thread. So, threads are lightweight processes within a process. In Java Habanero, threads can be acquired by either extending the Thread class or implementing the Runnable interface.

<h1>Problem statement</h1>
Finding the Minimum spanning tree in a data set using sequential implementation takes considerable time to accomplish in a relatively large data set, sometimes exponential, thereby leading to performance delay and utilization of memory for a longer time. The primitive method uses only a single thread of the system, does execute sequentially which leads other threads to remain idle. To decrease the overall task time, we try to utilize other threads as well, thus performing parallel computing.

The idea is to apply the concept of parallel programming using Borůvka’s algorithm for finding the weight of MST and further, the execution time to do so for the data set provided. The program is going to detect and utilize all the threads available for performing the task. This will minimize the execution time considerably.
The program also shows the relative speed bump due to parallelization as compared to the execution done sequentially.

<h1>Borůvka's algorithm</h1>
Borůvka’s Algorithm is a way to find a minimum spanning tree — a spanning tree where the sum of edge weights is minimized. It was the first algorithm developed (in 1926) to find MSTs; Otakar Borůvka used it to find the most efficient routing for an electrical grid.

There are many ways to find minimum spanning trees. Borůvka’s Algorithm is a greedy algorithm and is similar to Kruskal’s algorithm and Prim’s algorithm. It is basically a cross between the two algorithms. It is also known as Sollin’s algorithm, especially in computing.
Borůvka’s algorithm is based on the merging of disjoint components. At the beginning of the procedure, each vertex is considered a separate component. In each step, the algorithm connects (merges) every component with some other using strictly the cheapest outgoing edge of the given component (every edge must have a unique weight). This way it is guaranteed that no cycle may occur in the spanning tree.

Complexity of Borůvka’s algorithm is \\( O(\|E\|.log_{2}\|V\|) \\), where \\(E\\) is the number of edges, and \\(V\\)  is the number of vertices in \\(G\\)  (assuming \\( E ≥ V \\) )

A significant advantage of Borůvka’s algorithm is that it might be easily parallelized because the choice of the cheapest outgoing edge for each component is completely independent of the choices made by other components.

<h1>Psuedo code</h1>
1) Input is a connected, weighted, and undirected graph.

2) Initialize all vertices as individual components (or sets).

3) Initialize MST as empty.

4) While there are more than one component, do the following
for each component.

&nbsp;&nbsp;&nbsp;&nbsp;a) Find the closest weight edge that connects this
component to any other component.

&nbsp;&nbsp;&nbsp;&nbsp;b) Add this closest edge to MST if not already added.

5) Return MST.

<h1>Modules</h1>
This implementation of Boruvka’s MST was built on JAVA and uses Habanero Java Library for parallelism. 
Habanero-Java (HJ) is an innovative parallel programming model being developed at Rice University. Habanero-Java library (HJ-lib) is the new library implementation of HJ that can be used with any standard Java 8 implementation. The library-based approach is attractive since it does not require modifying a compiler as with language-based approaches.

HJ integrates a wide range of parallel programming constructs (e.g., async tasks, futures, data-driven tasks, for all, barriers, phasers, transactions, actors) in a single programming model that enables unique combinations of these constructs (e.g., nested combinations of task and actor parallelism). The orthogonal classes of parallel constructs enable programmers with a basic knowledge of Java to get started quickly with expressing a wide range of parallel patterns. HJ is capable of expressing many different forms of parallel patterns including data parallelism, pipeline parallelism, stream parallelism, loop parallelism, and divide-and-conquer parallelism. 
This code was tested on the High-Performance Multi-Core DaVinci system at Rice University. 

<h1>Implementation</h1>
To handle threading in parallel MST algorithm, the concurrent linked queue is used, as the threads can access the queue concurrently without consequences. The program detects the number of threads available for computing and in the pattern of 1, 2, 4, 6, etc. threads and initiates them. Each thread acts as an individual sequential implementation. In the case of the parallel algorithm, each thread tries to obtain a lock on a node and once it acquires the lock, it tries to obtain the lock on the connected nodes while checking whether the same is pre-acquired by another thread or has been accounted for or not.

According to the algorithm, the acquired nodes are added to the queue and finally, a single thread will contain the last node. All the threads are joined to get the final node’s total edges and weight, just like in a sequential algorithm. In this implementation, locks are used on components. Each thread gets a lock on the component in use. If the thread fails to obtain the lock, it signifies that another thread has already obtained the lock. Correctness of this implementation is achieved using a concurrent linked list and locks on components. This algorithm is deadlock-free, as any thread does not wait on the lock. The threads won’t get blocked on try lock, as it continues in case of failure, ensuring that the deadlock never occurs.

If any thread tries to obtain the lock on one of its component’s lock and succeeds, then the thread further tries to obtain the lock on connected components, and in case of failure, it simply continues its computation instead of waiting to obtain the lock on that component to avoid deadlock. The try Lock methods are concealed in a while loop which helps different threads to avoid livelocks. Threads would release the component if it fails to obtain the lock and would try lock again in another while loop iteration to avoid multiple threads colliding for locks. If two threads try to obtain the lock on the same multiple components, it won’t get stuck in livelock as only one thread will obtain locks on all the components, because of the while loop, before the other thread even obtains a lock on any other component.

<h1>Results</h1>
<h4><strong>A. Using DaVinci for Computing</strong></h4>

**Sequential**

Sequential test ran in 1354 ms on DaVinci.

**Single Thread**

Single threaded test ran in 1771 ms, 0.76x faster than sequential on DaVinci.

**2 Threads**

2 threaded test ran in 1372 ms, 1.69x faster than single-threaded on DaVinci.

**4 Threads**

4 threaded test ran in 923 ms, 2.51x faster than single- threaded on DaVinci.

**6 Threads**

6 threaded test ran in 813 ms, 2.85x faster than single- threaded on DaVinci.

**8 Threads**

8 threaded test ran in 802 ms, 2.89x faster than single- threaded on DaVinci.

**10 Threads**

10 threaded test ran in 769 ms, 3.01x faster than single-threaded on DaVinci.

**12 Threads**

12 threaded test ran in 814 ms, 2.85x faster than single- threaded on DaVinci.
<br/><br/>
<h4><strong>B. Using Local System for Computing</strong></h4>

**Sequential**

Sequential test ran in 1249 ms on Local System.

**Single Thread**

Single threaded test ran in 1931 ms, 0.64x faster than sequential on Local System.

**2 Threads**

2 threaded test ran in 1074 ms, 1.79x faster than single- threaded on Local System.

**4 Threads**

4 threaded test ran in 1021 ms, 1.89x faster than single- threaded on Local System.

<h1>Observations</h1>
It seems that 10 threads on DaVinci machine was faster than 12 threads on the same machine.
More number of threads doesn’t necessarily mean that the performance will increase.
Although it is true for most of the cases, the reason behind this is the same as increasing the number of threads doesn't decrease the computation time in the same ratio.

Like, If a process takes some time to complete its computation in a sequential algorithm, then doubling the number of the threads won’t half the computation time or speed up the computation twice.
The reason is initializing the threads take some time. So for more number of threads, the initializing of all the threads would take more time. And so the speedup may not be equally proportional.

So, Total Time = Time to initialize a thread * Number of threads + Time to compute / Number of threads.

In case of 12 threads, the time taken to initialize the 12 threads was more than the time taken to initialize 10 threads, where as the computation time wasn’t not a big difference. Therefore, 12 threads computation was slower than 10 threads computations. It can also be observed that the sequential algorithm completes faster than the single thread implementation. This is because of the code. The sequential algorithm is a simple Boruvka’s MST implementation. Whereas, the single thread implementation runs on the parallel Boruvka’s Algorithm, which takes care of the concurrency and obtains locks on the components. Therefore, it can be a slower algorithm for single thread but it is compatible with multiple threads unlike sequential algorithm.

Another possible reason could be, when there are too many cores working on the data, the rate of collision is increased, more threads collide as the algorithm progresses and only few connected components are left. So, incase of 12 cores, as the number of connected components decreases the collision between the threads increased and thus the performance decreases.
