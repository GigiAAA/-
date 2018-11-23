#### strncpy、strncmp、strncat模拟实现

```c
//strncpy
#include<stdio.h>
#include<windows.h>
#include<assert.h>
char *My_Strncpy(char *dst, char *src, int num)
{
	assert(dst);
	assert(src);
	char *dst_ = dst;
	while (num)
	{
		*dst = *src;
		dst++, src++;
		num--;
	}
	return dst_;
}
int main()
{
	char dst[] = "abcdefg";
	char src[] = "kkkk";
	int sz = strlen(src);
	char *p=My_Strncpy(dst, src, sz);
	printf("%s\n", p);
	system("pause");
	return 0;
}
```

```c
//strncmp
#include<stdio.h>
#include<windows.h>
#include<assert.h>
void My_Strncmp(char *dst, char *src, int sz, int len)
{
	if (sz != len)
		printf("两个字符串长度不同，字符串不相等!\n");
	else
	{
		while (*dst == *src)
		{
			dst++, src++;
		}
		if (*dst > *src)
		{
			printf("第一个字符串大\n");
		}
		else
		{
			printf("第二个字符串大\n");
		}
	}
}
int main()
{
	char dst[] = "abcdef";
	char src[] = "abcd12";
	int sz = strlen(dst);
	int len = strlen(src);
	My_Strncmp(dst, src, sz, len);
	system("pause");
	return 0;
}
```

```c
//strncat
#include<stdio.h>
#include<windows.h>
#include<assert.h>
char *My_Strncat(char *dst, char *src, int num)
{
	assert(dst);
	assert(src);
	char *dst_ = dst;
	while (*dst)
	{
		dst++;
	}
	while (num)
	{
		*dst = *src;
		dst++, src++;
		num--;
	}
	return dst_;
}
int main()
{
	char dst[] = "abcdefg";
	char src[] = "kkkk";
	int sz = sizeof(src)/sizeof(src[0]);
	char *p = My_Strncat(dst, src, sz);
	printf("%s\n", p);
	system("pause");
	return 0;
}
```

