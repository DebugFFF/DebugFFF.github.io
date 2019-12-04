# C语言

## 常见程序题

### 素数





### 正整数分解质因数







### 最大公约数和最小公倍数



### 回文数字





### 回文字符串



### 求立方根

```C
 double getLiFangGen(double num) {
		if (num == 0) {
			return num;
		}
		double num1,num2;
		num1 = num;
		num2 = (2*num1/3)+(num/(num1*num1*3));//利用牛顿迭代法求解  
		while(Math.abs(num2-num1)>0.000001){  
	        num1=num2;  
	        num2=(2*num1/3)+(num/(num1*num1*3));  
	    }  
	
	    return num2;  
	}
```

