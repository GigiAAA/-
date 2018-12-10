### "I am a Student"转换为"Student a am I"

问题思路：

（1）先整体翻转

（2）再逐个单词翻转

```c
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
#include<assert.h>

char *change_math(char *str, int len)
{
	char *start = str;
	char *end = str + len - 1;
	char temp;
	while (start < end)
	{
		temp = *start;
		*start = *end;
		*end = temp;
		start++;
		end--;
	}
	return str;
}

char *get_math(char *str, int len)
{
	assert(str != NULL);
	change_math(str, len);
	char *q = str;
	while (*str != '\0')
	{
		char *p = str;
		int num = 0;
		while ((*str != ' ') && (*str != '\0'))
		{
			str++;
			num++;
		}
		change_math(p, num);
		if (*str != '\0 ')
		{
			str++;
		}
	}
	return q;
}

int main()
{
	char str[20] = "student a am i";
	int len = strlen(str);
	get_math(str, len);
	printf("翻转后数组为:%s\n", str);
	system("pause");
	return 0;
}
```

![1](C:\Users\14665\source\repos\I am a Student\1.png)

