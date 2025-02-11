# 野指针和空悬指针

**面试高频指数：★★★☆☆**

野指针（Wild Pointer）和空悬指针（Dangling Pointer）都是指向无效内存的指针，但它们的成因和表现有所不同，区别如下：

#### 野指针（Wild Pointer）
野指针是一个未被初始化或已被释放的指针。
所以它的值是不确定的，可能指向任意内存地址。
访问野指针可能导致未定义行为，如程序崩溃、数据损坏等。
以下是一个野指针的例子：

```cpp
#include <iostream>

int main() {
    int *wild_ptr; // 未初始化的指针，值不确定
    std::cout << *wild_ptr << std::endl; // 访问野指针，可能导致未定义行为
    return 0;
}
```
#### 空悬指针（Dangling Pointer）
空悬指针是指向已经被释放（如删除、回收）的内存的指针。
这种指针仍然具有以前分配的内存地址，但是这块内存可能已经被其他对象或数据占用。
访问空悬指针同样会导致未定义行为。
以下是一个空悬指针的例子：

```cpp
#include <iostream>

int main() {
    int *ptr = new int(42);
    delete ptr; // 释放内存

    // 此时，ptr成为一个空悬指针，因为它指向的内存已经被释放
    std::cout << *ptr << std::endl; // 访问空悬指针，可能导致未定义行为
    return 0;
}
```

为了避免野指针和空悬指针引发的问题，我们应该：

1. 在使用指针前对其进行初始化，如将其初始化为`nullptr`。
2. 在释放指针指向的内存后，将指针设为`nullptr`，避免误访问已释放的内存。
3. 在使用指针前检查其有效性，确保指针指向合法内存。


