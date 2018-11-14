#### qsort函数排列字符串

```c
#include<stdio.h>
#include<windows.h>
#include<stdlib.h>   //qsort头文件
#include<search.h>   //qsort头文件
#include<assert.h>
int StringCom(const void *x_, const void *y_)
{
	assert(x_);
	assert(y_);
	char **x = (char **)x_;   // 原数组为char *的数组，其地址为char **类型
	char **y = (char **)y_;
	return strcmp(*x, *y);
}
int main()
{
	char* arr[] = { "dddd","fff","bb","aaaa" };
	int sz = sizeof(arr) / sizeof(arr[0]);
	qsort(arr, sz, sizeof(char*), StringCom);
	int i = 0;
	for (; i < sz; i++)
	{
		printf("%s\n", arr[i]);
	}	
	system("pause");
	return 0;
}
```

