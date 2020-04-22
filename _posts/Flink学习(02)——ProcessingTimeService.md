

## ProcessingTimeService

ProcessingTimeService是一个抽象类，里面定义了一组抽象方法。（感觉这个类应该定义成接口）

![image-20190910105707285](https://tva1.sinaimg.cn/large/006y8mN6ly1g6u8jjs4d5j30t60d2gno.jpg)



Defines the current processing time and handles all related actions, such as register timers for tasks to be executed in the future.
The access to the time via **getCurrentProcessingTime()** is always available, regardless of whether the timer service has been shut down. 
The registration of timers follows a life cycle of three phases:
In the initial state, it accepts timer registrations and triggers when the time is reached.
After calling quiesce(), further calls to registerTimer(long, ProcessingTimeCallback) will not register any further timers, and will return a "dummy" future as a result. This is used for clean shutdown, where currently firing timers are waited for and no future timers can be scheduled, without causing hard exceptions.
After a call to shutdownService(), all calls to registerTimer(long, ProcessingTimeCallback) will result in a hard exception.



![image-20190910094438550](https://tva1.sinaimg.cn/large/006y8mN6ly1g6u6g6dzidj31ex0jmgqc.jpg)