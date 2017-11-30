块的定义如下：

`return_type (^block_name) (parameters)`

为了使用方便，可以为块定义别名，这样就能像定义普通变量一样定义块，而且还能隐藏复杂的块类型。为块定义别名语法如下：

`typedef return_type (^block_name) (parameters);`

使用类型定义还会方便重构块的类型签名，因为一旦修改了块的结构，相关的调用处就会出现编译错误

