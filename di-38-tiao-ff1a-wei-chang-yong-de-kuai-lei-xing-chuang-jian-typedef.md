块的定义如下：

`return_type (^block_name) (parameters)`

为了使用方便，可以为块定义别名，这样就能像定义普通变量一样定义块，而且还能隐藏复杂的块类型。为块定义别名语法如下：

`typedef return_type (^block_name) (parameters);`

使用类型定义还会方便重构块的类型签名，因为一旦修改了块的结构，相关的调用处就会出现编译错误

在使用块类型的类中用typedef定义块，如果需要对外公开块类型，最好在块别名前加上类名

在不同的继承体系中如果用到了相同签名的块，需要在每个类里面单独起别名；如果在相同继承体系中，则在父类中定义块签名

