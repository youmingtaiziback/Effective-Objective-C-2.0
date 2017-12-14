# 第52条：别忘了NSTimer会保留其目标对象

创建timer的两种方式，无论哪种方式都需要有runloop，而且timer保留对象知道invalid

* 创建在当前runloop
* 先创建，然后再调度

所以重复的timer容易带来循环引用的问题





