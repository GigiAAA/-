### qsort函数

#### 定义：快速排序任意类型数据库函数。

#### 头文件：<stdlib.h>

#### qsort函数原型：

```c
void qsort(void *base,size_t num,size_t width,int (*compare)(const void *,const void *))
```

#### 各参数含义:

(1)base是待排序数组首元素地址；

(2)num是数组大小

(3)width是各元素占用空间大小；

(4)函数指针（回调函数）

#### 回调函数：

定义：回调函数就是一个通过函数指针调用的函数。如果你把函数的指针（地址）作为参数传递给另一个函数，当这个指针被用来调用其所指向的函数时，我们就说这是回调函数。

#### qsort函数应用：

```c
#include<stdio.h>
#include<windows.h>
#include<assert.h>
int MathCom(const void *x, const void *y)//回调函数MathCom比较相邻元素大小
{
	assert(x);
	assert(y);
	int *x_ = (int *)x;
	int *y_ = (int *)y;
	if (*x_ > *y_)
	{
		return 1;
	}
	else if (*x_ < *y_)
	{
		return -1;
	}
	else
	{
		return 0;
	}
}
void DisplayArr(int arr[], int sz)//打印数组
{
	assert(arr);
	int i = 0;
	for (; i < sz; i++)
	{
		printf("%d ", arr[i]);
	}
	printf("\n");
}
int main()
{
	int arr[] = { 1,4,5,6,958,67,-2,56,3 };
	int sz = sizeof(arr) / sizeof(arr[0]);
	printf("排序前:");
	DisplayArr(arr, sz);
	qsort(arr, sz, sizeof(int), MathCom);
	printf("排序后:");
	DisplayArr(arr, sz);
	system("pause");
	return 0;
}
```

#### 例题：模拟实现qsort函数。（用冒泡排序法）

##### 思路：

(1)构造MyQsort函数，模拟实现冒泡排序功能；

(2)构造回调函数判断任意两个元素大小；

(3)构造函数交换相邻两元素（以字节为单位）。

```c
//模拟qsort函数比较数字大小（回调函数）
//以字节为单位
#include<stdio.h>
#include<windows.h>
#include<assert.h>
int MathCom(const void *x,const void *y)//回调函数MathCom比较相邻元素大小
{
	assert(x);
	assert(y);
	int *x_ = (int *)x;
	int *y_ = (int *)y;
    //升序排列（若想改为降序排列，只需要将第一个if返回值改为-1，第二个if返回值改为1）
	if (*x_ > *y_)
	{
		return 1;
	}
	else if (*x_ < *y_)
	{
		return -1;
	}
	else
	{
		return 0;
	}
}
void _swap(void *x, void *y, int size)  //任意两个元素进行交换，以字节为单位
{
	assert(x);
	assert(y);
	char *x_ = (char*)x;
	char *y_ = (char*)y;
	while (size)
	{
		*x_ ^= *y_;
		*y_ ^= *x_;
		*x_ ^= *y_;
		x_++, y_++;     //每个字节依次交换，地址从小到大
		size--;
	}
}
void MyQsort(void *base, int count, int size, int(*MathCom)(void*,void*))
{
	assert(base);
	assert(MathCom);
	char *p = (char *)base;  // 将base强转为以字节为单位
	int i = 0;
	for (; i < count - 1; i++)   //控制冒泡次数
	{
		int j = 0;
		for (; j < count - 1 - i; j++)  //冒泡一次
		{
			if (MathCom(p + size * j, p + size * (j + 1))>0)  //判断连续两个元素大小
			{
				_swap(p + size * j, p + size * (j + 1), size);  //传连续两个元素的地址，进行交换
			}
		}
	}
}
void DisplayArr(int arr[], int sz)//打印数组
{
	assert(arr);
	int i = 0;
	for (; i < sz; i++)
	{
		printf("%d ", arr[i]);
	}
	printf("\n");
}
int main()
{
	int arr[] = { 1,4,5,6,958,67,-2,56,3 };
	int sz = sizeof(arr) / sizeof(arr[0]);
	printf("排序前:");
	DisplayArr(arr, sz);
	MyQsort(arr, sz,sizeof(int), MathCom);
	printf("排序后:");
	DisplayArr(arr, sz);
	system("pause");
	return 0;
}
```

