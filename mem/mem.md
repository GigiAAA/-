## memcpy与memmove函数异同

>memcpy
>
>memmove
>
>memset

#### memcpy

#### 函数原型

```c
void *memcpy(void *destination,const void *source,size_t num)
```

#### 头文件

```c
<string.h>
```

#### 作用：从源src所指的内存地址的起始位置开始拷贝num个字节到目标dest所指的内存地址的起始位置中。

#### 注意：

（1）memcpy是内存拷贝函数；

（2）此函数不考虑类型，以字节为单位进行拷贝；

（3）这个函数在遇到'\0'时不会停下来；

（4）memcpy与strcpy功能有所重叠，但拷贝字符串一般使用strcpy，因为strcpy以'\0'结尾，更加专业安全。

#### 模拟实现：

```c
#include<stdio.h>
#include<windows.h>
#include<assert.h>
void *My_Memcpy(void *dst, const void *src, int num)
{
	assert(dst);
	assert(src);
	char *dst_ = (char *)dst;
	char *src_ = (char *)src;
	while (num)
	{
		*dst_ = *src_;
		*dst_++;
		*src_++;
		num--;
	}
	return dst;
}
int main()
{
	char dst[] = "abcdef1234";
	char src[] = "kuj89";
	char *p=My_Memcpy(dst, src,strlen(src));
	printf("%s\n", p);
	system("pause");
	return 0;
}
```



### memmove

#### 函数原型：

```c
void *memmove(void *destination,const void *source,size_t num)
```

#### 头文件

```
<string.h>
```

#### 作用：功能几乎与memcpy相同，但memmove可处理内存重叠问题（源内存块和目标内存块可重叠）

##### 函数模拟实现分析：

![8](C:\Users\14665\source\repos\mem\8.png)

以上为七种数组内存存放方式，前两种内存没有重叠，可使用strcpy、strncpy、memcpy、memmove函数进行拷贝；第三种为源字符串首地址高于目标字符串首地址，故可正常将src中的字符串拷贝到dst中；第四种源字符串首地址低于目标字符串首地址，若从左至右拷贝（非memmove函数），第一个字符则会覆盖第二个字符，故会出现全a效果，若使用memmove函数进行拷贝，实际上是将字符串从右至左进行依次拷贝（当dst>src&&dst<src+len时确保dst首地址位于src之间）；第五种源字符串内存空间小于目标字符串内存空间，可直接进行拷贝；第六种源字符串内存大于目标字符串内存，故拷贝过程中会出现溢出，故此种内存重叠不存在；第七种为完全重叠，拷贝字符实际上是将字符拿出来再放回去，可正常进行拷贝。

##### 故内存重叠拷贝实际上只有两种，只有第四种内存重叠形式需要从右至左拷贝，其余形式均是从左至右进行拷贝。

#### 模拟实现：

```c
#include<stdio.h>
#include<windows.h>
#include<assert.h>
void *My_Memmove(char *dst, const char *src, int num)
{
	assert(dst);
	assert(src);
	if (dst > src&&dst<src + num)//right->left
	{
		char *dst_ = (char *)dst + num - 1;
		const char *src_ = (const char *)src + num - 1;
		while (num)
		{
			*dst_ = *src_;
			dst_--, src_--;
			num--;
		}
	}
	else//left->right
	{
		char *dst_ = (char *)dst;
		const char *src_ = (const char *)src;
		while (num)
		{
			*dst_ = *src_;
			dst_++, src_++;
			num--;
		}
	}
	return dst;
}
int main()
{
	char dst[32] = "abcdef1234";
	char str[32] = "abcdef1234";
	My_Memmove(dst + 1, dst, strlen(dst));
	printf("%s\n",dst);
	My_Memmove(str, str+1, strlen(str));
	printf("%s\n", str);
	system("pause");
	return 0;
}
```

程序结果：

![2](C:\Users\14665\source\repos\mem\2.png)

#### memcpy和memmove：

##### memcpy是将目标字符串中的num个字符按字节拷贝到源字符串中，memmove功能几乎与memcpy相同，但memmove可处理内存重叠问题。但经过验证最新memcpy函数也可处理内存重叠问题，可能是对memcpy函数做了改进。



#### memset

#### 函数原型：

```c
extern void *memset(void *buffer,int c,int count)
    //buffer:为指针或者数组
    //c:是赋给buffer的值
    //count:是buffer的长度
```

#### 头文件：

```c
<string.h>
```

#### 定义：将buffer中当前位置后面的count个字节用c替换并返回buffer。

#### 作用：是在一段内存中填充某个给定的值，它是对较大的结构体或数组进行清零的最快方法。

#### 常见误区：

1.memset函数以字节为单位进行操作；

2.可初始化为0或-1，但不能初始化为其它数。（原因是memset函数是以字节为单位进行操作，例如赋值1（int型），则每个元素的4个字节均会被设置为1）;

```c
#include<stdio.h>
#include<windows.h>
int main()
{
	int arr[10];
	int i = 0;
	memset(arr, 0, sizeof(arr));//初始化为0
    //memset(arr, -1, sizeof(arr));初始化为-1
    //memset(arr, 1, sizeof(arr));此方法不能初始化为-1和0以外的数字
	for (; i < 10; i++)
	{
		printf("%d ", arr[i]);
	}
	printf("\n");
	system("pause");
	return 0;
}
```

##### 结果为：

##### ![0](C:\Users\14665\source\repos\mem\0.png)![-1](C:\Users\14665\source\repos\mem\-1.png)![3](C:\Users\14665\source\repos\mem\3.png)