# C语言错题集



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