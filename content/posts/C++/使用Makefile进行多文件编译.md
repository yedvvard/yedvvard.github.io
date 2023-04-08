---
title: "使用Makefile进行多文件编译"
date: 2023-04-08T19:35:41+08:00
draft: false
toc: true
categories: ["C++"]
tags: ["C++","makefile"]
---

## 使用两个类class1和class2，在demo中利用class1访问class2的私有属性（基于friend）

class1.h
```cpp
#ifndef ININIIN
#define ININIIN
#include "class2.h"


class class1{
public:
    void print_class2(class2& cl2);
};

#endif
```

class2.h
```cpp
#ifndef ININIIN2
#define ININIIN2

class class2{
    friend class class1;//let class1 be friend of class2
public:
    class2(int b = 10):b_(b){};
private:
    int b_;
};

#endif
};

#endif
```
class1.cpp
```cpp
#include "class1.h"
#include "class2.h"
#include<iostream>
using std::cout;
using std::endl;

void class1::print_class2(class2& cl2){
    cout << cl2.b_ << endl;
};
```
class2.cpp
```cpp
#include "class2.h"
```

demo.cpp
```cpp
#include<iostream>
#include "class1.h"
#include "class2.h"
using std::cout;
using std::endl;


int main(){
    class1 cl1;
    class2 cl2;
    cl1.print_class2(cl2);
    return 0;
}
```

Makefile
```makefile
CC = g++ -std=c++11
CFLAGS = -g -Wall

demo: class1.o class2.o
	$(CC) $(CFLAGS) -o demo demo.cpp class1.o class2.o

class1.o: class1.h
	$(CC) $(CFLAGS) -c class1.cpp

class2.o: class2.h
	$(CC) $(CFLAGS) -c class2.cpp

clean:
	rm -rf demo *.o
```

make
```bash
$ make clean
rm -rf demo *.o

$ make      
g++ -std=c++11 -g -Wall -c class1.cpp
g++ -std=c++11 -g -Wall -c class2.cpp
g++ -std=c++11 -g -Wall -o demo demo.cpp class1.o class2.o

$ ./demo
10
```