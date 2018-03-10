title: 不重复随机序列生成算法
author: Walker
tags:
  - Algorthm
  - C
categories: []
date: 2017-08-23 23:41:00
---
如何生成一个0~n的不重复随机序列呢？是在《编程珠玑I》第一章的习题里面看到的，因为位图算法所需要的输入就是一个0～n的不重复随机序列。

那要怎么生成这么一个序列呢？最简单的算法就是不断重复生成一个0～n之间的随机数，如果该数字之前没有出现，则添加到结果序列中，如果出现过，则丢弃并重新生成随机数。可以看到这样子的算法是很简单的，但是，存在的去重操作太耗费时间了，当生成的随机数越来越多的时候，则重复的概率将越来越大。该算法的时间复杂度为O(N^2)，基本上不可能达到O(N)的效果。

接下来将介绍一种O(N)的算法，该算法不是考虑从无到有去构造一个随机序列，而是从一个有序序列构造生成一个随机序列。步骤如下：
1. 从序列一端（假设在位置n）开始，生成一个0～n的随机数k
2. 交换原序列中k和n两个位置的数
3. n-1（若从0端开始则n+1）后继续执行步骤1

通过不断的随机交换，我们便可以得到一个随机的序列，而原始序列已经保证元素是0～n有序不重复的，所以我们不需要执行任何去重的操作，只需要不断的交换交换交换最终就可以得到一个不重复随机序列，明显复杂度为O(N)。

下面为自己的实现，该程序使用的上面的算法，生成1～N的不重复随机序列，并将得到的序列保存到文件中（保存到文件中是因为《编程珠玑I》使用的序列是从文件中读取的）。
```
/* randomN.c */
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>
#include <stdlib.h>

void 
getList(int eleNum, FILE *fp) 
{
    int i;
    int *arr = (int *)malloc(sizeof(int) * eleNum);
    for ( i = 0; i < eleNum; i++ ) {
        arr[i] = i + 1;
    }
    for ( i = eleNum - 1; i > 0; i-- ) {
        int tmp = rand() % i;
        arr[tmp] = arr[i] + arr[tmp];
        arr[i] = arr[tmp] - arr[i];
        arr[tmp] = arr[tmp] - arr[i];
    }
    if ( fp == NULL ) {
        printf("error file");
    }
    for ( i = 0; i < eleNum; i++ ) {
        fprintf(fp, "%d\n", arr[i]);
    }
    free(arr);
}

int
main(int argc, char **argv)
{
    int N = atoi(argv[1]);
    FILE *fp;
    fp = fopen("test.txt", "wr+");
    getList(N, fp);
    fclose(fp);
    return 0;   
}
```
运行程序需要传入一个参数N，即序列元素的个数。