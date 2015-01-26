天气查询
=========
问题描述：

网友希望查询今天的天气预报，那么需要你写一个向服务器请求数据的程序，将气象呈现给网友。
现在有3个气象台都提供了气象数据， 这3个气象台分别为 :
A--中央气象台， 该气象台的特点是数据特别准确， 但是返回数据可能特别慢
B--北京市气象台 该气象台的特点是数据准确定很普通， 返回数据的速度也很普通
C--海淀区气象台 该气象台的特点是数据准确定很差， 但是数据返回的数据特别快。

你电脑上有一个文件， 这个文件里面就有上次查询的气象情况， 这个数据准确定是最最不准的， 但是获取到这个数据肯定最快的

注意: A虽然是特别慢， 但并不一定是最慢的， ，所以不能说查询速度是A<B<C， 只能说大部分情况下是查询速度A<B<C

给你的输入数据为 : A_URL, B_URL, C_URL, D_LOCAL_FILE_URL;

解决方案：

1.多个线程同时对A，B和C发起请求；

2.以C的响应时间为标准，考察A和B的响应时间；

   规则是：如果A的响应不超过C的2倍就认为是可接受的，就使用A的数据。
   在A的数据不可用的前提下，如果B的响应时间不超过C的1.5倍，就是用B的数据。
   
3.若C的响应时间过长，就认为A，B，C的数据都不可用，则使用D的数据。

规则3基于C的响应时间总是最短的这一前提。虽然说A，B，C三个源的响应时间并不总是A>B>C，不过根据题意以及经验，A和B的响应时间短于C的概率不大，因此可以认为前述的条件总是成立的。


这个程序由java语言完成，使用了两个类class climate和class multiThreads。

class climate包含一个main方法和一个check方法。

check方法负责对A，B，C三个连接的监听。

class multiThreads实现了Runable接口，并且重写了run方法。
