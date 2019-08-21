你如果要对自己刚刚搭建好的redis做一个基准的压测，测一下你的redis的性能和QPS（query per second）

redis自己提供的redis-benchmark压测工具，是最快捷最方便的，当然啦，这个工具比较简单，用一些简单的操作和场景去压测

1、对redis读写分离架构进行压测，单实例写QPS+单实例读QPS

redis-3.2.8/src

./redis-benchmark -h 192.168.31.187

-c <clients>       Number of parallel connections (default 50)
-n <requests>      Total number of requests (default 100000)
-d <size>          Data size of SET/GET value in bytes (default 2)

根据你自己的高峰期的访问量，在高峰期，瞬时最大用户量会达到10万+，-c 100000，-n 10000000，-d 50

