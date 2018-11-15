### 指针和数组经典题总和

```c
1.
#include<stdio.h>
#include<windows.h>
int main()
{
	char *c[] = { "ENIER","NEW","POINT","FIRST" };
	char **cp[] = { c + 3,c + 2,c + 1,c };
	char ***cpp = cp;
	printf("%s\n", **++cpp);//cpp=1  POINT
	printf("%s\n", *--*++cpp + 3);//++cpp=>cpp=2  --cpp->cpp=1(char *c[])  ER
	printf("%s\n", *cpp[-2] + 3);//(2)cpp-2->cpp=0    ST
	printf("%s\n", cpp[-1][-1] + 1);//(2)cpp-1->cpp=1   cpp-1->cpp=1(char *c[])  EW
	system("pause");
	return 0;
}
```

分析：char **cp[]为指向char *c[]的指针数组（反向），++cpp实际上有赋值，所以cpp值会改变，cpp-2没有赋值，值不会改变。

![8](C:\Users\14665\source\repos\Alto\8.png)

```c
2.
#include<stdio.h>
#include<stdlib.h>
int main()
{
	char *a[] = { "work","at","alibaba" };
	char **pa = a;
	pa++;
	printf("%s\n", *pa);
	system("pause");
	return 0;
}
```

![7](C:\Users\14665\source\repos\Alto\7.png)

```c
3.
#include<stdio.h>
#include<stdlib.h>
int main()
{
	int aa[2][5] = { 1,2,3,4,5,6,7,8,9,10 };
    //所有数组均为一维数组，在内存中以线性形式存放
	int *ptr1 = (int *)(&aa + 1);//&aa+1表示下一个数组的地址
	int *ptr2 = (int *)(*(aa + 1));//表示aa[1]的地址
	printf("%d,%d", *(ptr1 - 1), *(ptr2 - 1));//10    5
	system("pause");
	return 0;
}
```

![6](C:\Users\14665\source\repos\Alto\6.png)

```c
4.
#include<stdio.h>
#include<stdlib.h>
int main()
{
	int a[5][5];
	int(*p)[4];//int(*p)[4]为指向数组a[5][5]的指针数组，长度为4
	p = a;
	printf("%p,%d\n", &p[4][2] - &a[4][2], &p[4][2] - &a[4][2]);
    //%p为输出地址，为无符号整形，为-4的补码
    //两个指针相减结果为两个指针之间的元素个数，高地址指针减低地址结果为正数，低地址减高地址为负数
    //FFFFFFFC     -4
	system("pause");
	return 0;
}
```

![5](C:\Users\14665\source\repos\Alto\5.png)

```c
5.
#include<stdio.h>
#include<stdlib.h>
int main(int argc, char *argv[])
{
	int a[3][2] = { (0,1),(2,3),(4,5) };
    //逗号操作符，只输出最后一个表达式的结果，即该数组为1 3 5 0 0 0
	int *p;
	p = a[0]; //数组可整体初始化，但不能整体赋值。
	printf("%d", p[0]);//1
	system("pause");
	return 0;
}
```

![4](C:\Users\14665\source\repos\Alto\4.png)

```c
6.
#include<stdio.h>
#include<stdlib.h>
int main()
{
	int a[4] = { 1,2,3,4 };
	int *ptr1 = (int *)(&a + 1);
	int *ptr2 = (int *)((int)a + 1);
    //将a强转为int,+1实际上就是+1
	printf("%x,%x", ptr1[-1], *ptr2);
    //   00000004    02000000
    //电脑为小端，低地址处存放低数据（从左到右），读取从右到左
	system("pause");
	return 0;
}
```

![3](C:\Users\14665\source\repos\Alto\3.png)

```c
7.
#include<stdio.h>
#include<stdlib.h>
int main()
{
	int a[5] = { 1,2,3,4,5 };
	int *ptr = (int *)(&a + 1);
	printf("%d,%d", *(a + 1), *(ptr - 1));// 2  5
	system("pause");
	return 0;
}
```

![1](C:\Users\14665\source\repos\Alto\1.png)

