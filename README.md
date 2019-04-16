# C++ 智能指针
智能指针使用方法及注意事项

## 头文件
智能指针需要包含的头文件位 *<memory>*
  
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

### 4、从shared_ptr提供的类型转换（cast）函数的返回值构造

### 5、shared_ptr的“赋值”

### 6、shared_ptr的对象获取传统的 C 指针

### 7、shared_ptr的常见的其他用法

### 
  
