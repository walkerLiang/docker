title: 简单的位图排序算法
author: Walker
tags:
  - Algorithm
  - C
categories: []
date: 2017-08-23 23:41:00
---
位图算法是在《编程珠玑I》上看到的，该算法使用一个位代表一个数组中的其中一个值。例如要排序数值范围在1～32之间的数组时，我们可以使用一个int值，如果数值1存在，则将第一位置1，否则置0。最后我们可以根据每一位为0或者1来得到排序后的数组。
简单的排序算法如下：
```
/* bitmacSort.c */
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>

#define SIZE_INT (int)sizeof(int)

int
main(int argc, char **argv)
{
    int var, num = atoi(argv[2]), arr_idx, bit_idx, tmp;
    int bitmap_len = num / SIZE_INT;
    int *arr = (int *)calloc(bitmap_len + 1, SIZE_INT);   // 使用calloc申请内存，默认全为0。
    int count = 0;
    FILE *fd;
    if ( (fd = fopen(argv[1], "r")) == NULL ) {
        printf("open file error!\n");
        return 0;
    }
    while ( -1 != fscanf(fd, "%d", &var) ) {
        // 从文件中读取循环读取每一个数值，将每个数值对应的位置为1。
        arr_idx = var / SIZE_INT;
        bit_idx = var % SIZE_INT;
        tmp = 1 << bit_idx;
        arr[arr_idx] = arr[arr_idx] | tmp;
    }
    for ( arr_idx = 0; arr_idx < bitmap_len + 1; arr_idx++ ) {
        int i = 0;
        tmp = arr[arr_idx];
        for ( i = 0; i < SIZE_INT; i++ ) {
            if ( tmp & 1 ) {
                // 如果位为1，则打印出该位对应的数值。
                printf("%d ", arr_idx * SIZE_INT + i);
                count ++;
            }
            tmp = tmp >> 1;
        }
    }
    printf("\nnum count: %d\n", count);
    fclose(fd);
    free(arr);
    return 0;
}
```
该算法也可以用于其他数据类型的排序，但是需要使用一定的转换方式将其映射为int类型。此外，排序方式需要提前知道数值的范围提前分配好内存。