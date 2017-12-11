给一个实例添加成员变量时可以通过继承该类实现，但有时类的实例是通过某种机制创建的，无法子类化。这时可以使用“关联对象”

管理关联对象的相关方法：

```
void objc_setAssociatedObject(id object, const void * key, id value, objc_AssociationPolicy policy)
id objc_getAssociatedObject(id object, const void * key)
void objc_removeAssociatedObjects(id object)
```

#### 关联对象用法举例

```
#import <objc/runtime.h>

static void *EOCMyAlertViewKey = "EOCMyAlertViewKey";

- (void)askUserAQuestion {
    UIAlertView *alert = [[UIAlertViewalloc]
                          initWithTitle:@"Question"
                          message:@"What do you want to do?"
                          delegate:self
                          cancelButtonTitle:@"Cancel"
                          otherButtonTitles:@"Continue", nil];

    void (^block)(NSInteger) = ^(NSInteger buttonIndex){
        if (buttonIndex == 0) {
            [self doCancel];
        } else {
            [self doContinue];
        }
    };

    objc_setAssociatedObject(alert, EOCMyAlertViewKey, block, OBJC_ASSOCIATION_COPY);

    [alert show];
}

// UIAlertViewDelegate protocol method
- (void)alertView:(UIAlertView*)alertView clickedButtonAtIndex:(NSInteger)buttonIndex {
    void (^block)(NSInteger) = objc_getAssociatedObject(alertView, EOCMyAlertViewKey);
    block(buttonIndex);
}
```

相比delegate方式来讲代码更紧凑

