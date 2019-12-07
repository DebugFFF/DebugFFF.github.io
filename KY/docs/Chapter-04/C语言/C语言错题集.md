# C语言错题集



![image-20191203224406458](img/image-20191203224406458.png)



## switch

```C
#include <stdio.h>

int main () {
	int n= 'e';
	switch(n--)
	{
		default: printf("error");
		case 'a':
		case 'b': printf("good");break;
		case 'c': printf("pass");
		case 'd': printf("warn");
	}
	return 0;
}

```

执行结果为：

> error good

## 字符串的操作

- 比较 `int strcmp(const char* stri1，const char* str2);`  返回值为str1-str2
- 合并`char*strcat(char* desc, const char* src);`   desc目的，src源
- 复制 `char* strcpy(char* desc, const char* src);`



## 指向数组的指针

### 指向一维数组的指针

```C
int a[10] = {5,1,4,7,5,9,7,0,9,10};
int *p = a;// int *p; p = a;
*++a;  //*和++优先级相同，从右向左运算  先++a再取地址的值，也就是1(a[1])
```



### 指向二维数组的指针

```C
int a[M][N];
//指向二维数组a的指针如下
int (*q)[N] = a;//注意括号   int *q[4];这个是四个一维指针，而int (*q)[4];是二维指针，每一维有四个元素。
//q+1相当于下移一行，q+1 === a[1]
//想通过指针取到元素需要进行两次*运算，例如取到a[2][3]这个元素
*(*(q+2)+3)
```





## 指向函数的指针，和回调函数

```C
#include <stdio.h>
 
#define  GET_MAX 	0
#define  GET_MIN 	1
int (*p)(int,int); //定义指向函数的指针
int getMax(int i,int j)
{
	return i>j?i:j;
}
 
int getMin(int i,int j)
{
	return i>j?j:i;
}
 
int compare(int i,int j,int flag)
{
	int ret;
	//这里定义了一个函数指针，就可以根据传入的flag，灵活地决定其是指向求大数或求小数的函数
	//便于方便灵活地调用各类函数
	if(flag == GET_MAX){
        p = getMax; // p = &getMax
    }else{
        p = getMin; // p = getMin 
    }		
	ret = p(i,j);
	return ret;
}
 
int main()
{
	int i = 5,j = 10,ret;
	ret = compare(i,j,GET_MAX);
	printf("The MAX is %d\n",ret);
	ret = compare(i,j,GET_MIN);
	printf("The MIN is %d\n",ret);
	return 0 ;
}

```

