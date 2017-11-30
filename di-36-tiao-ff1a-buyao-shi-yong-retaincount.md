在ARC中`- (NSUInteger)retainCount OBJC_ARC_UNAVAILABLE;`已经被废弃，调用时如同调用retain、release、autorelease一样，编译器会报错。在MRC中仍可调用

不应该使用的原因：返回的计数只是某个时间点上的值，未考虑autoreleasepool的情况

有时系统会优化对象的释放行为，在计数为1时将其回收。如果不做优化，计数才会减至0

由字面值生成的NSString和NSNumber常量被视作单例，其引用计数很大。编译器在编译期直接把NSString常量放到二进制中，使用时直接读取。



