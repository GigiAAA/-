#### 问题：

实现一个函数，可以左旋字符串中的K个字符。

ABCD左旋一个字符得到BCDA

ABCD左旋两个字符得到CDAB

### 要点：因字符串长度有限，字符串旋转次数大于字符串长度时会重复，必须先求取实际旋转字符个数。

#### 方法一：

##### 思路：

（1）定义字符串。

（2）需注意字符串旋转次数可为N次（正整数）。（如旋转23次和旋转3次的结果一样）

（3）计算实际旋转次数

（4）写内层循环一次左旋

（5）加外层循环控制实际循环次数

```c
#include<stdio.h>
#include<windows.h>
void LeftMove(char array[],int len,int n)
{
	int num = n % len;  //n旋转次数可为任何整数，num为实际旋转次数
	int i = 0;
	for (; i < num; i++)
	{
		int j = 1;
		int temp = array[0];
		for (; j < len; j++)
		{
			array[j - 1] = array[j];
		}
		if (j = len - 1)
		{
			array[j] = temp;
		}
	}
}
int main()
{
	char array[] = "ABCD";
	int len = strlen(array);
	int n = -1;
	printf("请输入想左旋的字符个数:\n");
	scanf("%d", &n);
	printf("左旋前:%s\n",array);
	LeftMove(array, len, n);
	printf("左旋后:%s\n", array);
	system("pause");
	return 0;
}
```

#### 方法二：（优选，单层循环，时间复杂度为O（n））

##### 思路：

（1）从输入要翻转字符个数下标分为数组的前半部分和后半部分

（2）分别对前半部分、后半部分、整体进行翻转

```c
#include<stdio.h>
#include<windows.h>
#include<assert.h>
void Math(char array[],int i, int j)
{
    assert(array);
	while (i < j)
	{
		char temp = array[i];
		array[i] = array[j];
		array[j] = temp;
		i++;
	    j--;
	}
}
void LeftMove(char array[], int len, int n)
{
    assert(array);
	int num = n % len;
	int i = 0;
	Math(array,i, num - 1);
	Math(array,num, len - 1);
	Math(array,i, len- 1);
}
int main()
{
	char array[] = "ABCD";
	int len = strlen(array);
	int n = -1;
	printf("请输入想左旋的字符个数:\n");
	scanf("%d", &n);
	printf("左旋前:%s\n", array);
	LeftMove(array, len, n);
	printf("左旋后:%s\n", array);
	system("pause");
	return 0;
}
```

#### 指针方法实现：

```c
#include<stdio.h>
#include<windows.h>
#include<assert.h>
void Math(char* a, char* p)
{
	assert(a);
	assert(p);
	while (a < p)               //依次交换
	{
		*a ^= *p;
		*p ^= *a;
		*a ^= *p;
		a++;
		p--;
	}
}
void LeftMove(char *a, int len, int n)
{
	assert(a);
	int num = n % len;
	Math(a, a + num - 1);        //前半部分
	Math(a+num, a + len - 1);    //后半部分
	Math(a, a + len - 1);        //整体翻转
}
int main()
{
	char array[] = "ABCD";
	int len = strlen(array);
	int n = -1;
	printf("请输入想左旋的字符个数:\n");
	scanf("%d", &n);
	printf("左旋前:%s\n", array);
	LeftMove(array, len, n);
	printf("左旋后:%s\n", array);
	system("pause");
	return 0;
}
```

#### 方法三：（穷举法）

（缺点：需开辟空间，时间复杂度较高）

##### 思路：

   (1)利用malloc函数开辟空间

（2）利用strcpy拷贝数组a

（3）利用strcat拼接数组，形成双重数组

（4）根据实际旋转字符个数选择一段字符串输出

```c
#include<stdio.h>
#include<windows.h>
#include<assert.h>
void LeftMove(char *a, int len, int n)
{
	assert(a);
	int num = n % len;
	char *p = (char *)malloc(2 * len + 1);//开辟空间
	strcpy(p, a);//将数组a拷贝到p
	strcat(p, a);//将数组a拼接到p后面，得到双重数组a
	strncpy(a, p + num, len);//可以选择一段字符串输出
	free(p);//释放空间
}
int main()
{
	char array[] = "ABCD";
	int len = strlen(array);
	int n = -1;
	printf("请输入想左旋的字符个数:\n");
	scanf("%d", &n);
	printf("左旋前:%s\n", array);
	LeftMove(array, len, n);
	printf("左旋后:%s\n", array);
	system("pause");
	return 0;
}
```



