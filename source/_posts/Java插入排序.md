---
title: Java插入排序
date: 2018-11-19 22:39:29
tags: Java
---

Java插入排序
<!--more-->

```java
/**
插入排序
1. 默认第一个排好序；
2. 从第二个数开始，从后往前插空；
3. 外循环控制趟数，从第二个数开始往前插空，即array[1]，一直到最后一个数，即array[len-1]
4. 内循环，插空排序，
   从第二个数开始，array[1]它只需挪动一次或者不动
   array[2]第三个数需要0,1,2
   array[3]第四个数需要0,1,2,3
   array[4]第五个数需要0,1,2,3,4
   array[len-1]最后一数需要0,1,2,3，...，len
*/

public class InsertSort{
    public static void main(String[] args){
        int[] array = {8,2,5,9,10,7,1,3};
        
        insertSort(array);
        printArray(array);
    }

    public static int[] insertSort(int[] array){
        int len = array.length;
        for(int i=1; i<len; i++){
            for(int j=i; j>0 && array[j]<array[j-1]; j--){
                int m=array[j];
                array[j]=array[j-1];
                array[j-1]=m;
            }
        }
        return array;
    }

    public static void printArray(int[] array){
        for(int i=0; i<array.length; i++){
            System.out.print(array[i] + " ");
        }
    }


}
```