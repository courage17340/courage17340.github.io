---
layout: post
title:  "C++趣味代码"
date:   2023-08-26 20:00:00 +0800
categories: cpp
---

## 前言
本文记录一些比较有趣的C++代码，不过其实也不是C++专属

## 趋近于运算符

```cpp
int i = 5;
while (i --> 0) {
    printf("%d ", i);
}
```

```bash
4 3 2 1 0 
```

<details>
<summary>原理</summary>
其实-->是把--和>故意写在一起了
</details>

来源：忘了最初在哪看到的了，不过stackoverflow上面c++分类score次高的问题就是 [这个](https://stackoverflow.com/questions/1642028)

## sleep sort
如何给若干个整数排序是一个很常见的问题，但是总有人能整出新花样

```cpp
#include <chrono>
#include <cstdio>
#include <thread>
#include <vector>

using namespace std::chrono_literals;

int main() {
    std::vector<int> input = {2023, 8, 26, 42};
    std::vector<std::thread> threads;
    for (auto &x : input) {
        threads.emplace_back([x]() {
            std::this_thread::sleep_for(1ms * x);
            printf("%d\n", x);
        });
    }
    for (auto &t : threads) {
        t.join();
    }
}
```

```bash
8
26
42
2023
```

来源：同样不记得最初在哪看到的了，随便贴个 [stackoverflow链接](https://stackoverflow.com/questions/6474318)

## 另类数组访问
```cpp
#include <cstdio>

int main() {
    int a[4] = {1, 3, 5, 7};
    printf("%d\n", 1[a]);
}
```

```bash
3
```

C/C++中，默认的`[]`运算符可以认为是`a[n]`和`*(a + n)`等价，所以`1[a] = *(1 + a) = *(a + 1) = a[1] = 3`

可以参考 [这个回答](https://stackoverflow.com/questions/381542/with-arrays-why-is-it-the-case-that-a5-5a)
