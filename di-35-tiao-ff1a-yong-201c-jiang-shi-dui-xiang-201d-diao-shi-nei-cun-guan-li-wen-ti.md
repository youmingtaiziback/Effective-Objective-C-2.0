向一个已经被回收的对象发送消息时，可能会出现以下情况：

* 旧对象所在的内存未被占用，能够正常响应
* 旧对象所在的内存被部分占用，有可能响应，也有可能不响应
* 旧对象所在的内存完全被新对象占用，新对象有可能响应，也有可能不响应

开启“僵尸对象”功能后，runtime系统会把已经回收的对象转化成“僵尸对象”而不会真正回收他它们。这种对象所在的内存无法重用，僵尸对象收到消息后会抛出异常，准确说明收到的消息、描述回收之前的对象

给僵尸对象发消息时控制台的信息如下：

`*** -[CFString respondsToSelector:]: message sent to deallocated instance 0x713ebc0`

在Xcode里打开“僵尸对象”选项

![](/assets/import.png)

僵尸类是从名为\_NSZombie\_的模板类里复制出来的，僵尸类及僵尸对象的创建过程如下：

    // Obtain the class of the object being deallocated
    Class cls = object_getClass(self);

    // Get the class’s name
    const char *clsName = class_getName(cls);

    // Prepend _NSZombie_ to the class name
    const char *zombieClsName = "_NSZombie_" + clsName;

    // See if the specific zombie class exists
    Class zombieCls = objc_lookUpClass(zombieClsName);

    // If the specific zombie class doesn’t exist, then it needs to be created
    if (!zombieCls)
    {
        // Obtain the template zombie class called _NSZombie_
        Class baseZombieCls = objc_lookUpClass("_NSZombie_");

        // Duplicate the base zombie class, where the new class’s name is the prepended string from above
        zombieCls = objc_duplicateClass(baseZombieCls, zombieClsName, 0);
    }

    // Perform normal destruction of the object being deallocated
    objc_destructInstance(self);

    // Set the class of the object being deallocated to the zombie class
    objc_setClass(self, zombieCls);

    // The class of `self’ is now _NSZombie_OriginalClass

开启了“僵尸对象”后，runtime把dealloc替换成了以上版本

内存没有被释放，所以内存不可被复用

僵尸类的作用在消息转发中体现出来。\_NSZombie\_未实现任何方法，没有超类，只有一个isa成员变量

消息转发机制中，僵尸对象的处理流程如下：

```
// Obtain the object’s class
Class cls = object_getClass(self);

// Get the class’s name
const char *clsName = class_getName(cls);

// Check if the class is prefixed with _NSZombie_
if (string_has_prefix(clsName, "_NSZombie_")
{
    // If so, this object is a zombie

    // Get the original class name by skipping past the _NSZombie_, i.e. taking the substring from character 10
    const char *originalClsName = substring_from(clsName, 10);

    // Get the selector name of the message
    const char *selectorName = sel_getName(_cmd);

    // Log a message to indicate which selector is being sent to which zombie
    Log("*** -[%s %s]: message sent to deallocated instance %p", originalClsName, selectorName, self);

    // Kill the application
    abort();
}
```



