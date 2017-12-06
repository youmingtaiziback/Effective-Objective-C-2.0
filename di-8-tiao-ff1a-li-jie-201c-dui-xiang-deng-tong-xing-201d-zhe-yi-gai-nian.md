比较对象“等同性”时，==比较的是两个指针本身，如果要比较内容，应该用`NSObject`协议中的`isEqual:`，某些对象提出了特殊的“等同性判断方法”

```
NSString foo = @“Badger 123”;
NSString bar = [NSString stringWithFormat:@"Badger %i",123];
BOOL equalA = (foo == bar); // NO
BOOL equalB = [foo isEqual:bar]; //YES
BOOL equalC = [foo isEqualToString:bar]; //YES
```

NSObject协议中有两个判断等同性的方法：

```
- (BOOL)isEqual:(id)object;
- (NSUInteger)hash;
```

这两个方法的默认实现是：当且仅当“指针值”完全相等，这两个对象才相等。如果isEqual:判定两个对象相等，则hash方法肯定返回同一个值，反之不成立

hash方法的三种实现对比

```
- (NSUInteger)hash{
    return 1337;
}
```

在collection检索哈希表时，会用哈希码做索引。这种实现方式区分度太差，导致碰撞率极高

```
- (NSUInteger)hash{
    NSString *stringToHash = [NSString stringWithFormat:@"%@:%@:%i", _firstName, _lastName, age];
    return [stringToHash hash];
}
```

计算哈希码需要生成字符串，性能差

```
- (NSUInteger)hash{
    NSUInteger firstNameHash = [_firstName hash];
    NSUInteger lastNameHash = [_lastName hash];
    NSUInteger ageHash = _age;
    return firstNameHash ^ lastNameHash ^ ageHash;
}
```

既能保持较高效率，又能使哈希码位于一定范围内，碰撞率不至于太高

#### 特定类所具有的等同性判断方法

NSString、NSArray、NSDictionary都有各自的等同性判断方法，后两个方法传入错误类型会导致抛出异常

自己创建等同性判断方法的优势在于

* 无需检测参数类型，提高性能
* 可读性强

在编写自定义的等同性判断方法时，应该覆写“isEqual:”方法

```
- (BOOL)isEqualToPerson:(EOCPerson*)otherPerson{
    if (self == object) return YES;
    EOCPerson *otherPerson = (EOCPerson*)object;
    if (![_firstName isEqualToString:otherPerson.firstName])
        return NO;
    if (![_lastName isEqualToString:otherPerson.lastName])
        return NO;
    if (_age != otherPerson.age)
        return NO;
    return YES;
}

- (BOOL)isEqual:(id)object{
    if ([self class] == [object class]){
        return [self isEqualToPerson:(EOCPerson*)object];
    }else{
        return [super isEqual:object];
    }
}
```

#### 等同性判断的执行深度

深度等同性判断：像NSArray一样，先判断元素个数，如果相等，在逐个在每两个元素上调用`isEqual:`

如果对象是从数据库里的数据创建的，则只需要比较“主键”

#### 容器中可变类的等同性

对象放入collection之后就不应该改变其hash值了

```
NSMutableSet *set = [NSMutableSet new];
NSMutableArray *arrayA = [@[@1, @2] mutableCopy];
[set addObject:arrayA];
NSLog(@“set = %@“,set);
// set = {((1,2))}
```

```
NSMutableArray *arrayB = [@[@1, @2] mutableCopy];
[set addObject:arrayB];
NSLog(@“set = %@“,set);
// set = {((1,2))} 
```

```
NSMutableArray *arrayC = [@[@1] mutableCopy];
[set addObject:arrayC];
NSLog(@“set = %@“,set);
// set = {((1),(1,2))}  
```

```
[arrayC addObject:@2];
NSLog(@“set = %@“,set);
// set = {((1,2),(1,2))}  
```

```
NSSet *setB = [set copy];
NSLog(@“setB = %@“,setB);
// setB = {((1,2))} 
```



