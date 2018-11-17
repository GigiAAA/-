## Strstr函数

#### 定义：用于判断字符串str2是否是str1的子串。若是，返回str2在str1中首次出现的地址，反之，返回NULL。

#### 基本语法：

```c
char *strstr(const char*,const char*);
```

#### 头文件：

```c
<string.h>或<search.h>
```

模拟实现strstr函数：

```c
#include<stdio.h>
#include<windows.h>
#include<assert.h>
char *My_Strstr(const char *str1, const char *str2)
{
	assert(str1);
	assert(str2);
	char *str_q = str1;
	char *q = str_q;
	char *sstr_q = str2;
    //str1中若有与str2相等的字符，此时指针str_q指向相同首字符地址保持不变，指针p与指针sstr_q依次向后比，若sstr_q指向'\0',此时指针p指向有效字符（无越界），则表明str2是str1的子串，返回str_q（首元素地址）;若p与sstr_q依次向后比较时有不相同的字符，则指针q要归位至指针str_q处，再依次向后比较，指针sstr_q也要返回字符串首元素，便于下一次比较；若指针str_q遍历结束表明str2不是str1的子串，返回null。
	while (*str_q)
	{
		q = str_q;//长字符串中一部分与str2相等，后面不等时，q指针等于sttr_q
		sstr_q = str2;//指针归位
		while(*q&&*sstr_q&&(*q == *sstr_q))
		//判断str2是否为str1子串，按字节比较，若相等依次向后比较
		{
			q++;
			sstr_q++;
		}
		if (*sstr_q == '\0')
		//若str2结束str1还是指向有效字符，则str2是str1子串，输出第一个字符地址
		{
			return str_q;
		}
		str_q++;
	}
	if (*str_q == '\0')
	{
		return NULL;
	}
}
int main()
{
	char str1[] = "abcdef123kui123hutf";
	char str2[] = "1234";
	printf("%s\n", My_Strstr(str1, str2));
	system("pause");
	return 0;
}
```

![1](C:\Users\14665\source\repos\my_strstr\1.png)

