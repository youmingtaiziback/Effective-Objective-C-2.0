比较对象“等同性”时，==比较的是两个指针本身，如果要比较内容，应该用`NSObject`协议中的`isEqual:`，某些对象提出了特殊的“等同性判断方法”

NSString foo = @“Badger 123”;

NSString bar = \[NSString stringWithFormat:@"Badger %i",123\];

BOOL equalA = \(foo == bar\); // NO

BOOL equalB = \[foo isEqual:bar\]; //YES

BOOL equalC = \[foo isEqualToString:bar\]; //YES

