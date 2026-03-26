# C语言学习笔记

---

## 一、C语言基础

### 1.1 运行流程
**编写 → 编译 → 连接 → 运行**

```c
#include <stdio.h>  // 预处理
int main() {
    printf("Hello World");
    return 0;
}
```

---

### 1.2 基本语法

#### 关键字
> **定义**：特殊含义的英文字符，全部都是小写的。

#### 常量
> **定义**：程序执行的过程中值不会发生改变的数据。数据是数值不是计算过程。

**常量类型：**
- **整型常量**：整数
- **实型常量**：小数
- **字符常量**：单引号起来的字母数字和英文符号，只能有一个
- **字符串常量**：双引号起来的字符串常量

#### 输出格式说明符
| 数据类型 | 格式说明符 | 说明 |
|----------|------------|------|
| 整型     | `%d`       | 十进制整数 |
| 实数     | `%f`       | 浮点数 |
| 字符串   | `%s`       | 字符串 |
| 字符     | `%c`       | 单个字符 |

#### 变量
> **定义**：发生改变的数据可以定义为变量。

**使用规则：**
- 变量不可以重复定义
- 一条语句可以定义多个变量
- **先赋值，再使用**（必须遵守）

---

## 二、进制系统

### 2.1 进制表示法
| 进制 | 前缀 | 示例 |
|------|------|------|
| 二进制 | `0b` | `0b1010` |
| 八进制 | `0`  | `0123` |
| 十六进制 | `0x` | `0x1A` |

### 2.2 进制转换原理

#### 任意进制 → 十进制
**公式**：系数 × 基数的权次幂，最后相加

> **术语解释：**
> - **系数**：任意进制的当前位置的数值
> - **基数**：进制位
> - **权次幂**：从右往左从0开始的位置

#### 十进制 → 其他进制
**除基取余法**：对当前的数字不断地除以目标进制基数，得到的余数从下往上排列就是目标进制数字。

---

## 三、数据类型和运算符

### 3.1 数据类型

> [!tip] 提示
> `sizeof` 函数用来确定数据类型的大小。

#### 基本数据类型内存占用
| 数据类型        | 内存大小（字节） | 说明        |
| ----------- | -------- | --------- |
| `short`     | 2        | 短整型       |
| `int`       | 4        | 整型        |
| `long`      | 4 - 8    | 长整型（平台相关） |
| `long long` | 8        | 长长整型      |
| `float`     | 4        | 单精度浮点数    |
| `double`    | 8        | 双精度浮点数    |

#### 整数类型

> [!note] 重要特性
> - 整数类型默认是 `int` 类型
> - 数据类型的作用是能够存储不同类型的数据
> - 每个数据类型大小都不相同

**基本变量定义示例：**
```c
#include <stdio.h>
int main()
{
    int a = 1234123;
    int b = sizeof(a);  // 获取数据类型的大小
    printf("b = %d", b);
    return 0;
}
```

**完整数据类型形态：**
```c
#include <stdio.h>
int main()
{
    short int a = 1234123;  // 短整型
    long int t = 234;       // 长整型
    int b = sizeof(a);
    printf("b = %d", b);
    return 0;
}
```

**有符号和无符号类型：**
```c
#include <stdio.h>
int main()
{
    signed int a = 1234123;    // 有符号整数
    unsigned int b = 222;      // 无符号整数
    printf("u = %u", b);       // 无符号类型输出使用 %u
    return 0;
}
```

#### 小数类型
> [!note] 注意
> 小数的取值范围要比整数的取值范围要大。
> `unsigned` 不可以和整数类型以外的数据类型组合。

```c
#include <stdio.h>
int main() {
    float a = 3.14F;
    return 0;
}
```

#### 字符类型
`char` 类型占用一个字节。

---

### 3.2 标识符和键盘录入

#### 标识符规则
> [!tip] 标识符定义
> 标识符是代码中自己起的名称，用来命名变量。

**命名规则：**
1. 不能使用数字开头
2. 不可以是关键字
3. 区分大小写
4. 由数字、字母、下划线组成

---

#### 基本键盘录入
```c
#include <stdio.h>
int main() {
    int a;
    scanf("%d", &a);
    printf("a = %d", a);
    return 0;
}
```

#### 键盘录入细节

**示例1：混合输入**
```c
#include <stdio.h>

int main() {
    int age;
    char str[10];  // 字符串数组

    printf("请输入年龄：");  // 建议加上提示，用户体验更好
    scanf("%d", &age);

    printf("请输入字符串：");
    scanf("%s", str);  // 注意：字符串不需要 & 符号

    printf("年龄：%d\n", age);
    printf("字符串：%s\n", str);

    return 0;
}
```

**示例2：多个数值输入**
```c
#include <stdio.h>

int main() {
    int a;
    int b;
    scanf("%d %d", &a, &b);  // 输入数据时必须和双引号内容格式一致
    printf("a = %d, b = %d", a, b);
    return 0;
}
```

---

### 3.3 运算符

> [!tip] 运算特性
> - 小数计算是不精确的
> - 所有的非零数字都表示真（true）

#### 除法运算
```c
#include <stdio.h>
int main() {
    int a = 10;
    int b = 2;
    printf("%d", 10 / 2);
    return 0;
}
```

#### 取余运算（必须全部是整数）
```c
#include <stdio.h>
int main() {
    printf("%d", 10 % 3);
    return 0;
}
```

#### 运算符应用示例：提取数字各位
```c
#include <stdio.h>
int main() {
    int a = 1234;
    // 获取每一位数字：
    // 个位：a % 10
    // 十位：a / 10 % 10
    // 百位：a / 100 % 10
    // 千位：a / 1000 % 10
    printf("个位：%d\n", a % 10);
    printf("十位：%d\n", a / 10 % 10);
    printf("百位：%d\n", a / 100 % 10);
    printf("千位：%d\n", a / 1000 % 10);
    return 0;
}
```

---

### 3.4 数据类型转换

> [!tip] 类型转换规则
> - 根据数据类型的大小关系，数据类型小的与数据类型大的结合会让结果变成其中大的数据类型
> - `short`、`char` 类型完成运算的时候会先提升为 `int` 数据类型完成运算

```c
#include <stdio.h>
int main() {
    int a = 1234;
    short s1 = 10;
    short s2 = 24;
    short result = (short)(s1 + s2);  // 强制类型转换
    printf("size = %d", sizeof(result));
    return 0;
}
```

---

## 四、高级运算符

### 4.1 自增自减运算

#### 运算符类型
| 运算符 | 名称     | 说明                     |
|--------|----------|--------------------------|
| `++a`  | 先自增   | 先加1，再使用            |
| `--a`  | 先自减   | 先减1，再使用            |
| `a++`  | 后自增   | 先使用，再加1            |
| `a--`  | 后自减   | 先使用，再减1            |

> [!note] 先加后用
> 表示先对原始变量完成+1的操作，然后使用增加后的变量。

> [!note] 先用后加
> 表示先使用原始变量，然后将增加的数据给到原始变量中。

---

#### Windows平台机制
**前缀运算优先于后缀**：先统一完成自增自减运算，再把结果拿出来运算。后缀统一先用等表达式的变量，用完了再进行自增自减。

```c
#include <stdio.h>
int main() {
    int a = 10;
    int k1 = a++ + a++ + a;   // 10 + 10 + 10 = 30, a = 12
    int k2 = ++a + ++a + a;   // 14 + 14 + 14 = 42, a = 14
    int k3 = ++a + a++ + a;   // 15 + 15 + 15 = 45, a = 16
    int k4 = a++ + ++a + a;   // 17 + 17 + 17 = 51, a = 18
    return 0;
}
```

#### macOS/Linux平台机制
在Linux和macOS中，前缀和后缀的优先级是一样的，并且每一个前缀和后缀都是一个独立的个体。

```c
#include <stdio.h>
int main() {
    int i = 10;
    int j = 5;
    int k = i++ + ++i - --j - i--;
    printf("%d", k);
    return 0;
}
```

---

### 4.2 关系运算符
- `0` 表示 false（假）
- `1` 表示 true（真）

| 运算符 | 说明         |
|--------|--------------|
| `==`   | 等于         |
| `!=`   | 不等于       |
| `>`    | 大于         |
| `>=`   | 大于等于     |
| `<`    | 小于         |
| `<=`   | 小于等于     |

---

### 4.3 逻辑运算符

| 运算符 | 名称     | 说明                     |
|--------|----------|--------------------------|
| `&&`   | 逻辑与   | 同时满足                 |
| `\|\|` | 逻辑或   | 一个满足就是真           |
| `!`    | 逻辑非   | 将结果取反               |

#### 逻辑运算符应用示例
```c
#include <stdio.h>
int main() {
    // 要求：数字中不可以有7，且不是7的倍数
    int a;
    scanf("%d", &a);
    int ge = a % 10;        // 个位
    int shi = a / 10 % 10;  // 十位
    printf("%d", (ge != 7 && shi != 7 && a % 7 != 0));
    return 0;
}
```

#### 短路效果
当左边的表达式可以确定整个表达式的计算结果时，就直接结束程序。

- **`&&`（逻辑与）**：当出现第一个不满足条件的情况下，整个式子直接结束
- **`\|\|`（逻辑或）**：当出现第一个满足条件的情况下，整个式子直接结束

**示例1：逻辑与短路**
```c
#include <stdio.h>
int main() {
    int a = 1, b = 5;
    a > 0 && ++b;           // a>0为真，继续执行++b
    printf("a = %d, b = %d\n", a, b);  // 输出：a = 1, b = 6
    return 0;
}
```

**示例2：逻辑或短路**
```c
#include <stdio.h>
int main() {
    int a = 1, b = 5;
    a > 0 || ++b;           // a>0为真，短路，不执行++b
    printf("a = %d, b = %d\n", a, b);  // 输出：a = 1, b = 5
    return 0;
}
```

---

### 4.4 三元运算符（条件运算符）

#### 比较两个数字的最大值
```c
#include <stdio.h>
int main() {
    int a = 10;
    int b = 20;
    int c = a > b ? a : b;  // 如果a>b成立，取a，否则取b
    printf("max = %d", c);
    return 0;
}
```

#### 比较三个数字的最大值
```c
#include <stdio.h>
int main() {
    int a = 10;
    int b = 20;
    int c = 30;
    int temp = a > b ? a : b;        // 先比较a和b
    int final_max = temp > c ? temp : c;  // 再和c比较
    printf("max = %d", final_max);
    return 0;
}
```

---

### 4.5 逗号运算符

> [!tip] 特性
> - 从左往右执行
> - 优先级最低
> - 最后一个子表达式的结果是整个表达式的结果

```c
#include <stdio.h>
int main() {
    int i = 0;
    printf("%d", (i = 3, ++i, i++, i + 5));  // 结果为9
    return 0;
}
```

---

### 4.6 运算符优先级

> [!tip] 优先级规则
> - 小括号优先于所有
> - 一元运算符 > 二元运算符 > 三元运算符
> - `&&` > `\|\|` > 赋值运算符
> - **注意**：判断运算符中 `>=` 的优先级要高于 `!=`

#### 优先级题目解析

**题目1：三元运算符嵌套**
> **要点**：从左边的第一个问号开始找冒号，在过程中如果遇到了其他的问号，那么找冒号的次数+1（三元运算符的 `?` 和 `:` 是匹配的）

```c
#include <stdio.h>
int main() {
    int w = 4, x = 3, y = 2, z = 1;
    int number = w < x ? (w) : (z < y ? z : x);
    printf("number = %d", number);  // 输出：3
    return 0;
}
```

**题目2：嵌套三元运算符求最大值**
```c
#include <stdio.h>
int main() {
    int a = 3, b = 2, c = 1;
    int max = a > b ? (a > c ? a : c) : (b > c ? b : c);
    printf("max = %d", max);  // 输出：3
    return 0;
}
```

**题目3：逻辑运算符优先级**
```c
#include <stdio.h>
int main() {
    int a = 3, b = 4, c = 5;
    int num = a || (b + c && b - c);
    printf("num = %d", num);  // 输出：1
    return 0;
}
```

**题目4：复杂逻辑表达式**
```c
#include <stdio.h>
int main() {
    int a = 3, b = 4, c = 5;
    int num = !(((a < b) && !c) || 1);
    // 分析：((3<4) && !5) || 1 = (1 && 0) || 1 = 0 || 1 = 1
    // !1 = 0
    printf("num = %d", num);  // 输出：0
    return 0;
}
```

> [!tip] 小提示
> 确定优先级后对表达式左右完成括号，有助于理解运算顺序。

---

## 五、流程控制语句

### 5.1 IF 条件语句
```c
#include <stdio.h>
int main() {
    float temperature = 37.5;
    if (temperature > 40) {
        printf("体温过高");
    } else {
        printf("体温正常");
    }
    return 0;
}
```

### 5.2 SWITCH 多分支语句
```c
#include <stdio.h>
int main() {
    int choice = 1;
    switch (choice) {
    case 1:
        printf("选项1");
        break;
    case 2:
        printf("选项2");
        break;
    default:
        printf("默认选项");
        break;
    }
    return 0;
}
```

### for and while 循环

**==for 循环==**
>**包含** ：初始化 - 条件按表达式 - 自增表达式 - 循环体 
>**适合**：知道需要循环多少次结束。
```c
#include <stdio.h>
int main(){
	for (int i=0; i>10;i++)
	{
		printf("构思");
	}
}
```

**==while循环==**
>初始化 - 条件按表达式 - 自增表达式 - 循环体 
>**适合**：不知道需要循环多少次。

```c
#include <stdio.h>
int main(){
	int i = 0;
	while(i <10){
		printf("构思");
		i++；
	}
}

```

==**算法题解析**==

**第一题 反转数字**
>[!tip] 当前的题目需要将任意给的一个数字完成反转，题目的要点是是将原来的低位的数据变到高位（获取问题），其次在原始数据上去掉低位数字，最后完成转换后的拼接

```c
#include <stdio.h>

int main(){
    int a = 12345; // 原始变量
    int rev = 0; //  将原始变量完成转换后的结果
	 while (a != 0)
    {
        // 首先获取到个位
        int temp = a  % 10;
        // 获取到其他位置上的数字 , 并且要对原始的数据完成改变,因为下一次的改变需要使用这个
		a = a / 10;
        // 最后需要将当前的数字提升到最高位置上
	    rev = rev * 10 + temp;
    }
    printf("rev = %d",rev);
    return 0;
}
```
---
**第二题 2的次幂判断**
>[!tip] 判断是不是2的次幂首先要知道2的次幂首先是一个偶数，其次被2除到最后商是1
>

```c
#include <stdio.h>

int main(){
    // 判断一个数字是不是2的次幂
    int a = 2;
    int coumt = 0;
    while (a  % 2 ==0 && a > 1)
    {
        a /= 2;
    }
    if (a == 1)
    {
        printf("是2的次幂");
    }
    else{
        printf("不是2的次幂");
    }
    return 0;
}
```


**第三题 得到数字的算数平方根的整数部分**
>[!tip] 唯一需要注意的一点就是在while中的i在最后一次循环还会增加一次但是不参与下一次的代码运算

```C
#include <stdio.h>

int main()
{
    // 寻找算数平方根
    int a = 9;
    int i = 1;
    while (i * i <= a)
    {
        i++;
        printf("%d",i);
    }
    printf("result = %d",i - 1);
    return 0;
}
```

==do while ==
>[!tip] 先执行代码后执行判断无论怎样代码都会执行一次
```c
#include <stdio.h>
int main()
{
    int i = 1;
    do
    {
        printf("执行do while\n");
        i++;
    } while (i<=10);
    return 0;
}

```

### 循环高级部分

**==嵌套循环==**
```c
#include <stdio.h>
int main()
{
    for (int i = 1; i < 5; i++)
    {
        for (int j = i; j < 5; j++)
        {
            printf("*");
        }
        printf("\n");
    }
    return 0;
    // 第一次 i = 1 第一行 - 内部 1 - 5
    // 第二次 i = 2 第二行 - 内部 2 - 5

}
```

==**输出三角**==
```c
    for (size_t i = 0; i < 4; i++)
    {
        for (size_t j = 0; j <= i; j++)
        {
            printf("*");
        }
        printf("\n");
    }
```

**==输出口诀表==**
```c
    for (size_t i = 1; i <= 9; i++)
    {
        for (size_t j = 1; j <= i; j++)
        {
            printf("%d * %d = %d", i, j, (i * j));
        }
        printf("\n");
    }
    printf("goushi\t");
```

==判断质数==
```c
    #include <stdio.h>

int main()
{
    int number = 17;
    int count = 0;
    for (size_t i = 2; i < number; i++)
    {
        if (number % i == 0)
        {
            count++;
            break;
        }
    }
    printf("count = %d\n", count);
    if (count != 0)
    {
        printf("no 质数");
    }
    else
    {
        printf("yes");
    }
}
```
==质数==
```c
#include <stdio.h>

int main()
{
    int count_all = 0;                // 统计总量
    for (size_t i = 2; i <= 100; i++) // 判断范围
    {
        int count = 0;              // 统计当前数字是否是质数的变量
        for (int j = 2; j < i; j++) // 寻找当前数字书是否是质数
        {
            if (i % j == 0) // 进行判区间内有其他数字就停止
            {
                count++;
                break;
            }
        }
        if (count == 0) // 判断该当前数字是不是质数
        {
            count_all++; // 统计
        }
    }
    printf("all  = %d", count_all);
    return 0;

}

```

**==幂级数==**
>[!tip] 改变主要在   pow *= i 这句代码中内层控制循环次数后将幂的次方提升完成累加
```c
#include <stdio.h>

int main()

{
    long long sum = 0;               // 统计全部结果
    for (size_t i = 1; i <= 10; i++) // 外层次数
    {
        long long pow = 1;              //  统计当前次数的次方
        for (size_t j = 1; j <= i; j++) // 区间内的数字
        {
            pow *= i;
            // pow = pow * i;
            // 1  1*1
            // 2  1*2  2*2
            // 3  1*3  3*3
        }
        sum += pow;
    }
    printf("sum = %d", sum);
    return 0;
}
```
---
**==外部跳转==**
```c
#include <stdio.h>

int main()
{
    for (size_t i = 0; i < 5; i++)
    {
        for (size_t i = 0; i < 5; i++)
        {
            printf("构思\n");
            goto a;
        }
    }
a:printf("构思成功");
}
```
### 函数的注意点
>[!tip] 顺序执行，顶端定义

```c
#include <stdio.h>
int add(int a, int b);
int main()
{
    int result = add(10, 100);
    printf("%d", result);
    return 0;
}
int add(int a, int b)
{
    return (a + b);
}
```


**==设置随机数==**
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
int add(int a, int b);
int random(int origianl);
int main()
{
    int result = add(10, 100);
    printf("%d", result);
    
    int resultA = random(time(NULL));
    printf("resultA =%d", resultA);
    return 0;
}

int add(int a, int b)
{
    return (a + b);
}


int random(int origianl)
{
    srand(origianl);
    int a = rand();
    return a;
}
```


==限定范围==
>[!tip]
>1. 范围变成包头不包尾
>2. 尾 - 头
>3. 结果 + 需要确定的范围

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
// 随机 67 - 88 之间的数字
int main()
	srand(time(NULL));
	int a = rand() % (88 - 67) + 67;
	printf("%d",a);
}
```
### 数组
>[!tip] int arr [length];
>数组的默认数据0，字符  '\0' 字符串NULL

==**声明数组**==

```c
int arr1[80];
double arr [30];
```


**==数组的初始化==**

```c
int arr [] = {1,2,3}; // 数据的长度没有写长度等于数据量
```

**==数组遍历==**

```c
int arr[] = {1,2,3,4,5};
for(int i = 0; i< 5;i++)
{	
	printf("%d",arr[i]);
}
```

**==获得数组的首地址==**

```c
int arr[] = {1,2,3};
printf("%p\n",&arr+1);
// 首地址的偏移量
```

**==数组做为函数的参数传递==**

>[!tip] 数组作为函数的参数实际上传递的是数组的首地址
```c
  #include <stdio.h>

void bl(int arr[], int len)
{
    for (size_t i = 0; i < len; i++)
    {
        printf("%d", arr[i]);
    }
}
int main()
{
    int arr[] = {1, 2, 3};
    int len = sizeof(arr) / sizeof(int);
    bl(arr, len);
}
```


### 数组的算法题目

==最值==
```C
#include <stdio.h>
void bl(int arr[], int len, int a)
{
	int max = arr[1];
	int min = arr[1];
	if (a == 1)
	{
		for (int i = 0; i < len; i++)
		{
			arr[i] > max ? max = arr[i] : 0;
		}
		printf("max = %d", max);
	
	}
	else
	{

		for (int i = 0; i < len; i++)
		{
			arr[i] < min ? min = arr[i] : 0;
		}

		printf("min = %d", min);
	}

}
int main()
{
	int arr[] = {1, 2, 3, 4, 5, 6, 8};
	int len = sizeof(arr) / sizeof(int);
	bl(arr, len, 0);
}
```

**==求和==**
>[!tip] 创建一个随机函数，指定随机区间和数量，函数内部创建随机数据，通过临时数组保存，通过对随机数组比大小判断数组中的最大值
```c
int sum(int start, int stop, int len)

{
    int number_sum = 0;
    srand(time(NULL));
    int temp_arr[len];
    // 创建随机数据
    for (int i = 0; i < len; i++)
    {
        stop = (stop + 1) - start;
        int temp_number = rand() % stop + start;
        temp_arr[i] = temp_number;
    }

    for (size_t i = 0; i < len; i++)
    {
        number_sum += temp_arr[i];
        printf("I = %d\n", temp_arr[i]);
    }
    return number_sum;
}
```

```c
int main()
{
	int number_sum = sum(1,56,10);
	printf("sum = %d",numbrt_sum);
	return 0;
	
}
```

**==随机不相同==**

>[!tip]   首先是不断的生成随机数字，在数字存储到数组之前将当前数字与存储后的数组完成对比
>[[第二中写法]]

```C
int contains(int arr[], int len, int num);
int main()
{
    int arr[10] = {0};
    int len = sizeof(arr) / sizeof(int);
    srand(time(NULL));
    for (int i = 0; i < len;)
    {
        int num = rand() % 10 + 1;
        
        int flag = contains(arr, len, num);
        if (!flag)
        {
            arr[i] = num;
            i++; // 因为没有写判断不成功的的结果会出现判断掉过的情况将i++写在条件表达式中
        }
    }
    for (size_t i = 0; i < len; i++)
    {
        printf("i = %d \n", arr[i]);
    }
    return 0;
}
```
>[!tip]  将随机生成的数据完成具体的判断，返回判断结果
```c
int contains(int arr[], int len, int num)
{
    for (int i = 0; i < len; i++)
    {
        if (arr[i] == num)
        {
            return 1;
        }
    }
    return 0;
}
```
>[!tip] 反转数组中的数据
```c
int main(int argc, char *argv[]) {  
    int arr[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};  
    int len = sizeof(arr) / sizeof(int);  
  
    for (int i = 0; i < len; ++i) {  
        printf("i = %d\n", arr[i]);  
    }  
    int start = 0;  
    int stop = len - 1;  
  
    while (start < stop) {  
        int temp = arr[start];  
        arr[start] = arr[stop];  
        arr[stop] = temp;  
        start++;  
        stop--;  
    }  
    printf("-=-=-=-=-=--=-=-==-=-=");  
    for (int i = 0; i < len; ++i) {  
        printf("i = %d\n", arr[i]);  
    }  
}
```

>[!tip] 将数据打乱
```c
#include <stdio.h>  
#include <time.h>  
#include <stdlib.h>  
  
// 反转数组  
int main(int argc, char *argv[]) {  
    int arr[10] = {1, 2, 3, 4, 5, 6, 7};  
    const int len = sizeof(arr) / sizeof(int);  
  
    // 打乱数组中的数据  
    srand(time(NULL));  
  
    for (int i = 0; i < len; ++i) {  
        int index = rand() % len; //随机索引  
        int temp = arr[i];  
        arr[i] = arr[index];  
        arr[index] = arr[temp];  
    }  
  
    for (int i = 0; i < len; ++i) {  
        printf("i = %d\n", arr[i]);  
    }  
}
```

## 数据类型
### 查找算法

**==二分查找==**
>[!tip] 有序数据，每次查找排一半的查找范围,目的表示的是判断目标数据的可能位置，数据的左边数据的右边还是数据的中间
```c
int main(int argc, char *argv[]) {  
    int arr[] = {1, 2, 3, 5, 6, 20, 22, 34, 56};  
    int len = sizeof(arr) / sizeof(int);  
  
    int num = 5; // 首先是目标的数据  
    int min = 0; // 开始索引  
    int max = len - 1; // 结束索引  
  
    while (min <= max) {  
        // 中间索引  
        int mid = (min + max) / 2;  
  
        // 表示目标数据在右边  
        if (arr[mid] < num) {  
            min = mid + 1;  
        }  
        // 表示数据在左边  
        else if (arr[mid] > num) {  
            max = mid - 1;  
        }  
        // 表示目标数据和中间值是一样的  
        else {  
            printf("target index = %d", mid);  
            break;  
        }  
    }  
}
```
### 排序算法
**==冒泡排序==**
```c
  
int main() {  
    int arr[] = {1, 3, 4, 5, 2};  
    int len = sizeof(arr) / sizeof(int);  
    for (int i = 0; i < len - 1; ++i) {  
        // 轮次  
        for (int j = 0; j < len - 1 - i; ++j) {  
            // 每一轮比较刺激 -1 表示避免了索引越界， -i控制的是当前轮数比较的次数  
            if (arr[j] > arr[j + 1]) {  
                int temp = arr[j];  
                arr[j] = arr[j + 1];  
                arr[j + 1] = temp;  
            }  
        }  
    }  
}}
```

