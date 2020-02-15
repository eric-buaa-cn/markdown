## brpc

### ProfilerLinker

> #just for link ProfilerStart function
> Server(ProfilerLinker = ProfilerLinker());



### Socket

SocketId



### bthread_id_t and bthread::Id



### parking lot

worker pthread在空闲时，会"停"在parking lot中，等待被唤醒。

### butex

为什么有了futex，还需要创造butex?

futex是pthread之间的同步原语，并不能应用于bthread。我们需要一种同步原语，即能应用于bthread，又能应用于pthread。butex是用于bthread和pthread的32位同步原语。



### timer

bthread_timer_add在很多地方被调用，它是lock-free的吗？ 当在bthread中被调用时，是否会阻塞当前bthread所在的pthread?




问题

1. Server之间是如何共享bthread的
2. 