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



