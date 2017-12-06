类族模式可以隐藏抽象基类的实现细节。例如UIButton类可以根据type创建不同的button对象

#### 创建类族

```
#import <Foundation/Foundation.h>

typedef NS_ENUM(NSUInteger, EOCEmployeeType){
    EOCEmployeeTypeDeveloper,
    EOCEmployeeTypeDesigner,
    EOCEmployeeTypeFinance,
};

@interface HuEmployee : NSObject
@property(nonatomic, copy)NSString *name;
@property(nonatomic, assign)NSUInteger salary;

//1.定义类方法，根据不同type，返回同一父类对象
+(HuEmployee*)employeeWithType:(EOCEmployeeType)type;
-(void)doWork;
@end
```

```
@implementation EOCEmployee

//2.抽象基类没有特殊标识，一般不定义init方法 也不实现抽象函数，各自在子类里实现
+(EOCEmployee*)employeeWithType:(EOCEmployeeType)type
{
    switch (type) {
        case EOCEmployeeTypeDeveloper:
            return [EOCEmployeeDeveloper new];
            break;
        case EOCEmployeeTypeDesigner:
            return [EOCEmployeeDesigner new];
            break;
        case EOCEmployeeTypeFinance:
            return [EOCEmployeeFinance new];
            break;
        default:
            break;
    }
    return nil;
}

-(void)doWork
{
    //2.1抛出一个异常，避免在基类里面实现
    NSException *e = [NSException
                      exceptionWithName: @"exceptionName"
                      reason: @"必须在子类实现改方法"
                      userInfo: nil];
    @throw e;
}

@end
```

```
@interface EOCEmployeeDeveloper : EOCEmployee

@end

@implementation EOCEmployeeDeveloper

-(void)doWork
{
    [self writeCode];
}

-(void)writeCode
{
    /////
}

@end
```

以上的工厂模式是创建类族的方法之一

Objective-C没有办法指明某个基类是“抽象的”，只能在文档中写明。基类一般没有名为init的方法，还可以通过在基类的方法里面抛出异常来保证用户不会使用基类实例

如果对象所属的类位于类族中，调用\[obj isMemberOfClass:\[A class\]\]时就要注意了，因为此时obj的类可能是A的子类

#### Cocoa里的类族

系统框架中有很多类族。大部分collection都是类族

```
NSArray *array = [NSArray array];
if ([array class] == [NSArray class]) {

}
```

这个判断不可能为真，因为array所属的类是抽象基类NSArray的某一个子类

如果要判断的话，可以采用

```
NSArray *array = [NSArray array];
if ([array isKindOfClass:[NSArray class]) {

}
```

对于Cocoa中NSArray这样的类来说，可以新增子类，但要遵守以下规则

* 子类应该继承自类族中的抽象基类
* 子类应该定义自己的数据存储方式
* 子类应当覆写超累文档中指明需要覆写的方法

在类族中实现子类时所需遵循的规范一般都会定义于基类的文档之中

