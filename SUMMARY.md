# Summary

* [Introduction](README.md)
* [第1章 熟悉Objective—C ](shu-xi-objective-c.md)
  * [第1条：了解Objective—C语言的起源 ](le-jie.md)
  * 第2条：在类的头文件中尽量少引入其他头文件 
  * 第3条：多用字面量语法，少用与之等价的方法 
  * 第4条：多用类型常量，少用\#define预处理指令 
  * 第5条：用枚举表示状态、选项、状态码 
* 第2章 对象、消息、运行期 
  * 第6条：理解“属性”这一概念 
  * 第7条：在对象内部尽量直接访问实例变量 
  * [第8条：理解“对象等同性”这一概念 ](di-8-tiao-ff1a-li-jie-201c-dui-xiang-deng-tong-xing-201d-zhe-yi-gai-nian.md)
  * [第9条：以“类族模式”隐藏实现细节 ](di-9-tiao-ff1a-yi-201c-lei-zu-mo-shi-201d-yin-cang-shi-xian-xi-jie.md)
  * 第10条：在既有类中使用关联对象存放自定义数据 
  * 第11条：理解objc\_msgSend的作用 
  * 第12条：理解消息转发机制 
  * 第13条：用“方法调配技术”调试“黑盒方法” 
  * 第14条：理解“类对象”的用意 
* 第3章 接口与API设计 
  * 第15条：用前缀避免命名空间冲突 
  * 第16条：提供“全能初始化方法” 
  * 第17条：实现description方法 
  * 第18条：尽量使用不可变对象 
  * 第19条：使用清晰而协调的命名方式 
  * 第20条：为私有方法名加前缀 
  * 第21条：理解Objective—C错误模型 
  * 第22条：理解NSCopying协议 
* 第4章 协议与分类 
  * 第23条：通过委托与数据源协议进行对象间通信 
  * 第24条：将类的实现代码分散到便于管理的数个分类之中 
  * 第25条：总是为第三方类的分类名称加前缀 
  * 第26条：勿在分类中声明属性 
  * 第27条：使用“class—continuation分类”隐藏实现细节 
  * 第28条：通过协议提供匿名对象 
* 第5章 内存管理 
  * 第29条：理解引用计数 
  * 第30条：以ARC简化引用计数 
  * 第31条：在dealloc方法中只释放引用并解除监听 
  * 第32条：编写“异常安全代码”时留意内存管理问题 
  * 第33条：以弱引用避免保留环 
  * [第34条：以“自动释放池块”降低内存峰值 ](di-34-tiao-ff1a-yi-201c-zi-dong-shi-fang-chi-kuai-201d-jiang-di-nei-cun-feng-zhi.md)
  * [第35条：用“僵尸对象”调试内存管理问题 ](di-35-tiao-ff1a-yong-201c-jiang-shi-dui-xiang-201d-diao-shi-nei-cun-guan-li-wen-ti.md)
  * [第36条：不要使用retainCount ](di-36-tiao-ff1a-buyao-shi-yong-retaincount.md)
* [第6章 块与大中枢派发 ](di-6-zhang-kuai-yu-da-zhong-shu-pai-fa.md)
  * [第37条：理解“块”这一概念 ](di-37-tiao-ff1a-li-jie-201c-kuai-201d-zhe-yi-gai-nian.md)
  * [第38条：为常用的块类型创建typedef ](di-38-tiao-ff1a-wei-chang-yong-de-kuai-lei-xing-chuang-jian-typedef.md)
  * [第39条：用handler块降低代码分散程度 ](di-39-tiao-ff1a-yong-handler-kuai-jiang-di-dai-ma-fen-san-cheng-du.md)
  * 第40条：用块引用其所属对象时不要出现保留环 
  * 第41条：多用派发队列，少用同步锁 
  * 第42条：多用GCD，少用performSelector系列方法 
  * 第43条：掌握GCD及操作队列的使用时机 
  * 第44条：通过Dispatch Group机制，根据系统资源状况来执行任务 
  * 第45条：使用dispatch\_once来执行只需运行一次的线程安全代码 
  * 第46条：不要使用dispatch\_get\_current\_queue 
* 第7章 系统框架 
  * 第47条：熟悉系统框架 
  * 第48条：多用块枚举，少用for循环 
  * 第49条：对自定义其内存管理语义的collection使用无缝桥接 
  * 第50条：构建缓存时选用NSCache而非NSDictionary 
  * 第51条：精简initialize与load的实现代码 
  * 第52条：别忘了NSTimer会保留其目标对象

