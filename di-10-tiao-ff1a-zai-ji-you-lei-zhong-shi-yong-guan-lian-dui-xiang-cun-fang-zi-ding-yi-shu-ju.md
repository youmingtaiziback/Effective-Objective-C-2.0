给一个实例添加成员变量时可以通过继承该类实现，但有时类的实例是通过某种机制创建的，无法子类化。这时可以使用“关联对象”

管理关联对象的相关方法：

```
void objc_setAssociatedObject(id object, const void * key, id value, objc_AssociationPolicy policy)
id objc_getAssociatedObject(id object, const void * key)
void objc_removeAssociatedObjects(id object)
```



