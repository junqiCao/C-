# C++ 智能指针
智能指针使用方法及注意事项

## 头文件
智能指针需要包含的头文件位    <memory>
  
## shared_ptr的构造

### 1、使用空参数构造函数

  template<typename T>
  shared_ptr<T> ptr;
  
此时ptr是一个nullPtr指针，当对一个空指针进行操作时，会导致异常。

### 2、使用new操作符的返回值构造

  shared_ptr<T> ptr(new T(100))
  
为ptr创建具有100个T类型的内存空间

### 3、使用复制构造函数（或等号重载），从其他shared_ptr的对象构造

  shared_ptr<T> ptr1(ptr) //这里使用了复制构造函数的方法，会使ptr的引用计数加1
shared_ptr可以当做函数的参数传递，或者单做函数的返回值返回，这个时候其实相当于使用复制构造函数。

### 4、从shared_ptr提供的类型转换（cast）函数的返回值构造

shared_ptr 也可以类型转换，在共享指针里面的类型转换可以使用这种方式

  shared_ptr<B> ptrb(new B())
  shared_ptr<A> ptra(dynamic_pointer_cast<A>(ptrb))
  

### 5、shared_ptr的“赋值”

shared_ptr 也可以直接赋值，但是必须是赋给相同类型的 shared_ptr 对象，而不能是普通的 C 指针或 new 运算符的返回值。
当共享指针 a 被赋值成 b 的时候，如果 a 原来是 NULL, 那么直接让 a 等于 b 并且让它们指向的东西的引用计数加 1。
如果 a 原来也指向某些东西的时候，如果 a 被赋值成 b, 那么原来 a 指向的东西的引用计数被减 1, 而新指向的对象的引用计数加 1。

  shared_ptr<T> a(new T());
  shared_ptr<T> b(new T());
  a = b; // 此后 a 原先所指的对象会被销毁，b 所指的对象引用计数加 1
  
当shared_ptr的对象在构造之后，可以被赋予空值，此时需要使用reset()函数
  shared_ptr<T> a(new T());
  a.reset();  // 此后 a 原先所指的对象会被销毁，并且 a 会变成 NULL
  
### 6、shared_ptr的类型转换

shared_ptr 有两种类型转换的函数，一个是 static_pointer_cast, 一个是 dynamic_pointer_cast

  shared_ptr<A> ptra;
  shared_ptr<B> ptrb(new B());
  ptra = dynamic_pointer_cast<A>(ptrb);

  
### 7、shared_ptr的对象获取传统的 C 指针
  
  shared_ptr<T> ptr(new T());
  T *p = ptr.get(); // 获得传统 C 指针


### 
  
