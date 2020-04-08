---
title: C语言中的冒泡排序简单介绍
date: 2020-04-03 10:55:10
categories: C语言
tags: C
---


简介：

冒泡排序是一种比较简单地排序算法。

它重复走过要排序的数列，一次比较两个元素，如果他们的值不一样，就把它们交换过来。直到没有数据需要进行交换，数列中的数据已经排序完成。

这种算法的名字因为越大的元素会经由交换慢慢浮到数列的前端，故名“冒泡排序”。



排序的代码结构：


``` 
void nums_sort(int nums[],int count){

	int i,j,temp;
	for(i=0;i<count-1;i++){
		for(j=0;j<count-1-j;j++){
			if(nums[j]>nuns[j+1]){

			  	temp=nums[j];			
				nums[j]=nums[j+1];
				nums[j+1]=temp;
			}
		}
	}
}
``` 