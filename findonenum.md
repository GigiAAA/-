### 写一个函数返回参数二进制中 1 的个数？

#### 方法一：

思路：（1）输入一个整数，构造函数。

​           （2）将数字与1按位与，将数字二进制序列右移或者1左移均可，统计1的个数即可。

```c
#include<stdio.h>
#include<windows.h>
int FindOneNum(unsigned int n)
{
	int count = 0;
	int flag_ = 1;
	while (n)
	{
		if (n & flag_)
		{
			count++;
		}
		n >>= 1;
	}
	return count;
}
int main()
{
	unsigned int n = 0;
	printf("请输入一个整数:\n");
	scanf("%d", &n);
	int ret=FindOneNum(n);
	printf("%d\n", ret);
	system("pause");
	return 0;
}
```

#### 方法二：（最优解）

思路：（1）输入一个整数，构造函数。

​           （2）数字n与n-1按位与一次，会将数字n低比特位的1消除，统计按位与次数即为原数字二进制序列中1的个数。

```c
举例：（二进制）100-1->011&100->000
             1010 1000-1->1010 0111 & 1010 1000 ->1010 0000
             1010 0000-1->1001 1111 & 1010 0000 ->1000 0000
             1000 0000-1->0111 1111 & 1000 0000 ->0000 0000     3个1
```

```c
#include<stdio.h>
#include<windows.h>
int FindOneNum(unsigned int n)
{
	int count=0;
	while (n)
	{
		n &= n-1;  //将n与n-1异或赋予n
		count++;
	}
	return count;
}
int main()
{
	int n = 0;
	printf("请输入一个整数\n");
	scanf("%d", &n);
	int ret=FindOneNum(n);
	printf("%d\n", ret);
	system("pause");
	return 0;
}
```

