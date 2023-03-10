
---
title: 如何判断机器的字节顺序是高字节在前还是低字节在前
date: 2020-01-27 17:55:23
tags:
---
> 经常听各种人在群里面讨论各种机，linux，mac，windows，单片机的啥都有。讨论的焦点就是在这些机器上到底是高字节在前还是低字节在前。
> 其实这个问题是很简单，只要稍微懂一点c语言知识。对，只要知道如何使用指针就可以做出正确的判断了。甚至你也许连指针都不会也没关系。只要你的电脑上有一个c的编译器，随便百度或者google以下判断的代码，拷贝黏贴上去，然后在运行一下，什么问题都可以搞定了

``` c
#include <stdio.h>

int main() {

    int  x  =  1;
    if(*(char  *)&x  ==  1)
        printf("低字节在前\n");
    else
        printf("高字节在前\n");

    return 0;
}
```

本机的运行结果：
![](QQ20220509-132106.png)

**代码解释说明：**

1. 1是整型，在不同机器上，可能是16位，也可能是32位，即2字节或4字节。假设是4字节。(如图左边是高字节，右边是低字节)
![](QQ20220509-132120.png)


2. C语言中只有char是单字节数据，所以，只有通过(char )地址这种方式，才能查看某个确切地址空间上的数据。

3. 在低字节在前的机器上，1在内存空间中的二进制形式是
![](QQ20220509-132133.png)


这时候令x=1的话，&x是x的地址，即指向0x01这个字节，通过 (char )&x得到的是1。
在高字节在前的机器上，1在内存中是

![](QQ20220509-132144.png)

&x指向的是0x00这个字节，(char )&x得到的0