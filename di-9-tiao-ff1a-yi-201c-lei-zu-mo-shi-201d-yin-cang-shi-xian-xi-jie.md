类族模式可以隐藏抽象基类的实现细节。例如UIButton类可以根据type创建不同的button对象

#### 创建类族

```
#import <Foundation/Foundation.h>

typedef NS_ENUM(NSUInteger, EOCEmployeeType){
    HuEmployeeTypeDeveloper,
    HuEmployeeTypeDesigner,
    HuEmployeeTypeFinance,
};

@interface HuEmployee : NSObject
@property(nonatomic, copy)NSString *name;
@property(nonatomic, assign)NSUInteger salary;

//1.定义类方法，根据不同type，返回同一父类对象
+(HuEmployee*)employeeWithType:(EOCEmployeeType)type;
-(void)doWork;
@end
```



