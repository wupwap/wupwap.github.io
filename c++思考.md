# c++思考
## namespace
1. Namespace in C++ is the declarative part where the scope of identifiers like functions, the name of types, classes, variables, etc., are declared. The code generally has multiple libraries, and the namespace helps in avoiding the ambiguity that may occur when two identifiers have the same name.
2. https://www.simplilearn.com/tutorials/cpp-tutorial/cpp-namespaces#:~:text=Namespace%20in%20C%2B%2B%20is%20the%20declarative%20part%20where,occur%20when%20two%20identifiers%20have%20the%20same%20name.
## reference VS pointer
1. https://www.geeksforgeeks.org/pointers-vs-references-cpp/
> 指针是单独的一个个体，这个个体存储其他对象的地址，编译的过程中遇到指针时，我们要通过这个指针的信息取获取到对应的对象，这个信息可以随意修改；而引用是一个别名，在编译的过程中，这个引用的操作实际上就是对该对象的操作，大概流程应该是这样：我把一个对象赋给一个引用时，以后编译的过程中，如果遇到这个引用的操作就是对该对象的操作，不管该对象被移动到哪里，引用都会定位到它，编译完成后，该别名就不存在了。

> 对指针和引用的操作，都是对原对象的操作。

> 当指针指向一个对象时，如果这个对象的地址更改了，那该指针就访问不到了，因为它存储的是原来的地址；而引用是，告诉编译器，我就是这个对象，不管这个对象的地址换到那啦，你都要帮我定位到。

> 指针定位到地址；引用定位到名字。
## 心得
1. 默认生成的析构函数不会主动释放指针所指向的对象内存
2. 当指向一个对象的引用或指针离开作用域时，析构函数不会执行
3. 只会自动释放栈内空间，c++中，除了new创建的对象存储在堆内，其他均存储在栈中，当离开作用域时，该作用域的所有使用的栈内空间都将被释放，而个别指针或引用指向的堆中空间并不会被释放。
4. 默认的析构函数执行的逻辑则是，我只释放我能主宰的，比如它的整个对象都是在我本身的内存中的，这样我不必考虑他人，我可以自由释放，有问题他人负责，但是指针所指向的对象内存不归我管，我不能释放，释放了别人就有问题，你得负责。
5. 需要析构函数的类也需要拷贝和赋值操作，为什么？因为需要析构函数意味着有指向对象的指针需要我们自己释放，因为默认的析构函数不会帮我们释放，而我们如果想要释放指向对象的指针，那就要保证该指针所指向的对象只被我们一个人指向，否则我们释放了别人就有问题啦，怎么保证呢？即走进来和走出去都要管控，走进来即通过拷贝构造函数创建对象时，我们不能按照默认的拷贝构造函数只复制指针，而是要构建我们自己的构造函数，同理，默认的赋值操作也只简单的复制指针，我们要有自己的赋值操作函数。
6. 需要拷贝操作的类也需要赋值操作，反之亦然
## 左值、右值
1. https://www.jianshu.com/p/94b0221f64a5
## 异常处理
1. https://zhuanlan.zhihu.com/p/406894769