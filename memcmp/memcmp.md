### strcmp、strncmp和 memcmp的异同

### strcmp

#### 函数原型：

```c
int strcmp(const char *str1,const char *str2)
```

#### 头文件：

```c
<string.h>
```

#### 返回值：

若str1==str2,则返回零；

若str1>str2,则返回1；

若str1<str2,则返回-1。

#### 作用：按照ASCII码,逐字符比较str1和str2，若字符相同依次向后，若第一次字符出现不同，ASCII码大的字符串大,与字符串长度无关。

#### 模拟实现:

```c
#include<stdio.h>
#include<windows.h>
#include<assert.h>
int My_Strcmp(char *str1, const char *str2)
{
	assert(str1);
	assert(str2);
	int ret = 0;
	while (!(ret=*(unsigned char*)str1 - *(unsigned char*)str2)&&*str1&&str2)
	{
		++str1, ++str2;
	}
	if (*str1 > *str2)
	{
		return 1;//字符串str1大
	}
	else if (*str1 < *str2)
	{
		return -1;//字符串str1小
	}
	else
	{
		return 0;
	}
}
int main()
{
	char str1[] = "abcd123";
	char str2[] = "abcd123";
	int n = My_Strcmp(str1, str2);
	printf("%d\n", n);
	system("pause");
	return 0;
}
```

### strncmp

#### 函数原型

```c
int strncmp(const char*str1,const char *str2,int num)
```

#### 头文件：

```c
<string.h>
```

#### 返回值：

若str1==str2,则返回零；

若str1>str2,则返回1；

若str1<str2,则返回-1。

#### 作用：比较str1和str2字符串的前num个字符。

#### 模拟实现：

```c
#include<stdio.h>
#include<windows.h>
#include<assert.h>
int My_Strncmp(char *str1, const char *str2, int num)
{
	assert(str1);
	assert(str2);
	while (num)
	{
		if(!((*str1-*str2) && *str1&&*str2))//保证str1、str2不为空
		{
			str1++,str2++;
		}
		num--;
	}
	if (*str1 > *str2)
	{
		return 1;//str1字符串大
	}
	else if (*str1 < *str2)
	{
		return -1;
	}
	else
	{
		return 0;
	}
}
int main()
{
	char str1[] = "abcdef123";
	char str2[] = "abcd123";
	int n = My_Strncmp(str1, str2, sizeof(str2));
	printf("%d\n", n);
	system("pause");
	return 0;
}
```

### memcmp

#### 函数原型：

```c
int memcmp(const void *ptr1,const void *ptr2,size_t num)
```

#### 头文件：

```c
<string.h>或<memory.h>
```

#### 返回值：

若str1==str2,则返回零；

若str1>str2,则返回1；

若str1<str2,则返回-1。

#### 作用：比较内存区域ptr1和ptr2的前num个字符。memcmp功能与strncmp几乎相同，但由于memcmp是以字节进行比较（ASCII码），故可处理特殊情况。例如，一个字符串中如有多个\0（ASCII码对应为数字0），strncmp函数遇到第一个\0就会停止，memcmp函数可全部比较。

#### 模拟实现：

```c
#include<stdio.h>
#include<windows.h>
#include<assert.h>
int main()
{
	char str1[] = "12'\0'3";
	char str2[] = "1234";
	int n;
	n = memcmp(str1, str2, sizeof(str1));
	if (n > 0)
	{
		printf("'%s'is greater than '%s'.\n",str1, str2);
	}
	else if(n<0)
	{
		printf("'%s'is less than '%s'.\n", str1, str2);
	}
	else
	{
		printf("'%s'is same as '%s'.\n", str1, str2);
	}
	//printf("%s\n", strncmp(str1, str2, sizeof(str2)));
	system("pause");
	return 0;
}
```

#### 注意：memcmp对字符串中的\0会转为ASCII码0对待，不会影响\0之后的比较。

