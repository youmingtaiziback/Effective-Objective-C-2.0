在ARC中`- (NSUInteger)retainCount OBJC_ARC_UNAVAILABLE;`已经被废弃，调用时如同调用retain、release、autorelease一样，编译器会报错。在MRC中仍可调用

不应该使用的原因

* 返回的计数只是某个时间点上的值，未考虑autoreleasepool的情况



