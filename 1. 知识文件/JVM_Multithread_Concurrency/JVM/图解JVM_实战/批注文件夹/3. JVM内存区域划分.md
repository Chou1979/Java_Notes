
> [!PDF|] [[004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】.pdf#page=2&selection=14,11,15,23|004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】, p.2]]
> > JVM在运行代码时，必须使用多块内存空间，且不同的内存空间用来放不同的数据， 配合写的代码流程才能让系统运行

> [!PDF|] [[004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】.pdf#page=3&selection=7,2,12,17|004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】, p.3]]
> > 	方法区：存放类相关信息
> > 	
> > 		这个方法区是在JDK 1.8以前的版本里，代表JVM中的一块区域，主要是放从“.class”文件里加载进来的类，还会有一些类似常量池的东西放在这个区域里。
> > 		在JDK 1.8以后，这块区域的名字改了，叫做“Metaspace”，可以认为是“元数据空间”这样的意思，存放自己写的各种类相关的信息。
> 
> 自己的猜测：估计是翻译成“方法区”容易产生歧义，让人以为是存放方法相关信息的地方。


> [!PDF|] [[004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】.pdf#page=3&selection=18,2,18,15|004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】, p.3]]
> > 	程序计数器：用来记录当前执行的字节码指令的位置（执行到了哪一条字节码指令）
> 
> 		通过字节码执行引擎，执行编译好的，面向计算机的，class字节码文件中的字节码指令
> 
> 扩展：
> > [!PDF|] [[004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】.pdf#page=5&selection=4,5,6,44|004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】, p.5]]
> > 	JVM是支持多个线程的，所以其实你写好的代码可能会开启多个线程并发执行不同的代码，所以就会有多个线程来并发的执行不同的代码指令因此每个线程都会有自己的一个程序计数器，专门记录当前这个线程目前执行到了哪一条字节码指令
> 
> 


> [!PDF|] [[004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】.pdf#page=5&selection=9,2,9,10|004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】, p.5]]
> > 	Java虚拟机栈：保存方法内的局部变量数据
> 
> 扩展：
> > [!PDF|] [[004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】.pdf#page=6&selection=6,0,10,1|004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】, p.6]]
> > 		每个线程都有自己的Java虚拟机栈，比如main线程就会有自己的一个Java虚拟机栈，用来存放自己执行的那些方法的局部变量。
> > 		如果线程执行了一个方法，就会对这个方法调用创建对应的一个栈帧，并压入该线程自己的虚拟机栈中；当方法调用完毕时，该栈帧就会出栈。
> > 		栈帧里有这个方法的局部变量表、操作数栈、动态链接、方法出口等东西，这里大家先不用全都理解，我们先关注局部变量
> 
> 
> 
> 


> [!PDF|] [[004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】.pdf#page=8&selection=0,2,0,9|004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】, p.8]]
> > 	Java堆内存：存放各种实例化的对象
> 
> 扩展：
> > [!PDF|] [[004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】.pdf#page=9&selection=0,0,3,57|004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】, p.9]]
> > 	Java堆内存区域里会放入类似ReplicaManager的对象，因为在main方法里创建了ReplicaManager对象，那么在线程执行main方法代码的时候，就会在main方法对应的栈帧的局部变量表里，让一个引用类型的“replicaManager”局部变量来存放ReplicaManager对象的地址。相当于你可以认为局部变量表里的“replicaManager”指向了Java堆内存里的ReplicaManager
> 
> 
> 
> 


> [!PDF|] [[004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】.pdf#page=9&selection=6,2,6,14|004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】, p.9]]
> > 	核心内存区域的全流程串讲（尽可能自己复述这部分内容）
> 


> [!PDF|] [[004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】.pdf#page=11&selection=5,2,5,8|004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】, p.11]]
> > 	其他内存区域：本地方法栈，存放各种native方法（本地操作里的非java代码）的局部变量表之类的信息。


[[!PDF|]] [[004、大厂面试题：JVM中有哪些内存区域，分别都是用来干嘛的【JAD资源网丨www.jiuandun.com】.pdf#page=12&selection=10,2,11,3&color=yellow|p.12]]
>> 思考题：