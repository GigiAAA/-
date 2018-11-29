#### 问题描述：

喝汽水，1瓶汽水1元，2个空瓶可以换一瓶汽水，给20元，可以买多少汽水。

##### 问题思路：

（1）可以确保的是有多少钱就可以喝多少瓶汽水；

（2）计算空瓶数，只要空瓶数大于1，就可以换取汽水。

```c
#include<stdio.h>
#include<windows.h>
int popNumber(unsigned int money)
{
	int pop = money;
	int empty = money;
	while (empty>1)
	{
		pop += empty / 2;
		empty = empty / 2 + empty % 2;
	}
	return pop;
}
int main()
{
	unsigned int money = 0;
	printf("请输入金钱数:>\n");
	scanf("%d", &money);
	int ret=popNumber(money);
	printf("%d\n", ret);
	system("pause");
	return 0;
}
```

![1](C:\Users\14665\source\repos\c语言喝汽水问题\1.png)

**还有另外一种思路（可参考）**

因最终停止换汽水的时候，人手里肯定是有一个空瓶子的。假如今天你有20块钱，一瓶汽水一块钱，两个空瓶子可以换取一瓶汽水，也就是说一块钱可以买两个空瓶子，20块钱可以买40个空瓶子。

除去最后留下来的一瓶汽水外，剩下的39瓶空瓶子均会归还给店家，即买了39瓶。

```c
#include<stdio.h>
#include<windows.h>
int popNumber(unsigned int money)
{
	int pop = money;
	return pop*2-1;
}
int main()
{
	unsigned int money = 0;
	printf("请输入金钱数:>\n");
	scanf("%d", &money);
	int ret = popNumber(money);
	printf("%d\n", ret);
	system("pause");
	return 0;
}
```

![2](C:\Users\14665\source\repos\c语言喝汽水问题\2.png)

