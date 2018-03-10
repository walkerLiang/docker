title: 数组左移算法
author: Walker
tags:
  - Algorithm
  - C
categories: []
date: 2017-08-26 18:06:00
---
之前也看到过该算法，但是那篇博客上并没有讲到原理，今天又在《编程珠玑I》上看到了，其实原理非常简单，就是数组乘法的转置而已。可以将要移位的数组x分为a和b两个部分，即x=ab，则移位后的数组为y=ba。

存在以下公式：ba=(a<sup>r</sup>b<sup>r</sup>)<sup>r</sup>

故我们可以先将a反转，b反转，再将整个数组反转，最后便可以得到移位的数组。这个算法比一个一个左移相对简单多了，因为但移位多的话，耗时比较多。

下面为自己写的实现：
```
/* reverseAB */
#include <stdio.h>
#include <stdlib.h>

int
main()
{
    int arr[] = {1,4,6,8,3,5,9,3,5,6,1,9,4};
    int len = sizeof(arr) / sizeof(int);
    int k = 5, i, idx_i, idx_j;   // 0~4为a，4~13为b
    for ( i = 0; i < len; i++ ) {
        printf("%d ", arr[i]);
    }
    printf("\n");
    for ( i = 0; i < k / 2; i++ ) {
    	// 反转a
        idx_i = i;
        idx_j = k - 1 - i;
        arr[idx_i] = arr[idx_i] + arr[idx_j];
        arr[idx_j] = arr[idx_i] - arr[idx_j];
        arr[idx_i] = arr[idx_i] - arr[idx_j];
    }
    for ( i = 0; i < (len - k + 1) / 2; i++ ) {
    	// 反转b
        idx_i = i + k;
        idx_j = len - i - 1;
        arr[idx_i] = arr[idx_i] + arr[idx_j];
        arr[idx_j] = arr[idx_i] - arr[idx_j];
        arr[idx_i] = arr[idx_i] - arr[idx_j];
    }
    for ( i = 0; i < len / 2; i++ ) {
    	// 反转整个数组
        idx_i = i;
        idx_j = len - i - 1;
        arr[idx_i] = arr[idx_i] + arr[idx_j];
        arr[idx_j] = arr[idx_i] - arr[idx_j];
        arr[idx_i] = arr[idx_i] - arr[idx_j];
    }
    for ( i = 0; i < len; i++ ) {
        printf("%d ", arr[i]);
    }
    printf("\n");
    return 0;
}

```