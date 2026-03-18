# C语言学习笔记

## 运行流程

**编写 → 编译 → 连接 → 运行**

```c
#include <stdio.h>  // 预处理
int main() {
    printf("Hello World");
    return 0;
}
```
## 基本语法

### 关键字
特殊含义的英文字符，全部都是小写的。

### 常量
程序执行的过程中值不会发生改变的数据。数据是数值不是计算过程。

**常量类型：**
- 整型常量
- 实型常量
- 字符常量：单引号起来的字母数字和英文符号，只能有一个
- 字符串常量：双引号起来的字符串常量

### 输出格式说明符
| 数据类型 | 格式说明符 |
|----------|------------|
| 整型     | %d         |
| 实数     | %f         |
| 字符串   | %s         |
| 字符     | %c         |

### 变量
发生改变的数据可以定义为变量，变量不可以重复定义，一条语句可以定义多个变量。

**使用条件**：先赋值，再使用。

---

## 进制系统

### 进制表示法
- 二进制：`0b`开头（如 `0b1010`）
- 八进制：`0`开头（如 `0123`）
- 十六进制：`0x`开头（如 `0x1A`）

### 进制转换原理

#### 任意进制 → 十进制
**公式**：系数 × 基数的权次幂，最后相加

- **系数**：任意进制的当前位置的数值
- **基数**：进制位
- **权次幂**：从右往左从0开始的位置

#### 十进制 → 其他进制
**除基取余法**：对当前的数字不断地除以目标进制基数，得到的余数从下往上排列就是目标进制数字。

# 数据类型和运算符

## 数据类型

> **提示**：`sizeof` 函数用来确定数据类型的大小。

### 基本数据类型内存占用
| 数据类型 | 内存大小（字节） |
|----------|------------------|
| short    | 2                |
| int      | 4                |
| long     | 4 - 8            |
| long long| 8                |
| float    | 4                |
| double   | 8                |

### 整数类型

> **提示**：
> - 整数类型默认是 `int` 类型
> - 数据类型的作用是能够存储不同类型的数据
> - 每个数据类型大小都不相同

#### 基本变量定义
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

#### 完整数据类型形态
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

#### 有符号和无符号类型
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

### 小数类型
小数的取值范围要比整数的取值范围要大。

> **注意**：`unsigned` 不可以和整数类型以外的数据类型组合。

```c
#include <stdio.h>
int main() {
    float a = 3.14F;
    return 0;
}
```

### 字符类型
`char` 类型占用一个字节。

### 标识符和键盘录入

#### 标识符规则
> **提示**：标识符是代码中自己起的名称，用来命名变量。
> - 不能使用数字开头
> - 不可以是关键字
> - 区分大小写
> - 由数字、字母、下划线组成

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

---

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

### 运算符

> **提示**：
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

### 数据类型转换

> **提示**：
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
# 高级运算符

### 自增运算

|先自增|先自减|后自增|后自减|
|---|---|---|---|
|++a|--a|a++|a--|
|||||
|||||

---

<aside> 💡

**先加后用** : 表示先对原始变量完成+1的操作然后使用增加后的变量

</aside>

<aside> 💡

**先减后用**: 表示先使用原始变量然后将增加的数据给到原始变量中

</aside>

**win机制 ：**前缀的运算优先于后缀，先统一的完成自增自减运算再次把结果拿出来运算，后缀统一先用等表达式的变量用完了在进行自增自减

```c
#include <stdio.h>
int main(){
	int a = 10;
	// 在这需要注意等到用完了在进行自增，最后还是使用了变量a还不可以
	int k1 = a++ + a++ +a; // 10+10 +10 = 30 , a=12
	int k2 = ++a + ++a +a; // 14 +14 +14 = 42 a = 14
	int k3 = ++a + a++ +a; // 15 + 15 +15 =45 a = 16
	int k4 = a++ + ++a +a； // 17 +17 +17 = 51 a = 18
}
```

**mac linux**

在linux和mac中的前缀和后缀的优先级是一样的，并_且_每一个前缀和后缀都是一个独立的个体

```c
#include <stdio.h>
int main(){
	int i = 10;
	int j = 5;
	int k = i++ + ++i - --j - i--;
	printf("%d",k)
}
```

### 关系运算符

0 ： false

1 ： true

|==|！=|>|>=|<|<=|
|---|---|---|---|---|---|

### 逻辑运算符

|&&|11|！|
|---|---|---|
|同时满足|一个满足就是真|将结果取反|
|结果为true的情况下|||

```c
#include <stdio.h>
int main(){
	// 首先要求数字中不可以有7
	// 其次数据中不可以有7的倍数
	int a;	
	scanf("%d",&a);
	int ge = a % 10;
	int shi = a / 10 %10;
	printf("%d",(ge !=7 && shi !=7 && a % 7 !=0));
}
```

**短路效果**

- ****当左边的表达式可以确定整个表达式的计算 就直接结束程序
- &&（ 同时满足）：当出现第一个不满足条件的情况下那么整个式子直接结束
- || （只有一个满足）：当出现第一个条件是满足的情况下整个式子结束

```c
#include <stdio.h> 
int main(){
	int a =1 ,b=5;
	a>0 && ++b;
	printf("a=%d, b= %d\\n"a,b);  // 输出的结果是1 ，6
}
```

```c
#include <stdio.h>
int main(){
	int a = 1,b=5;
	a>0 || ++b;
	printf("x=%d,y=%d\\n" ,a,b); // 输出的结 a = 1 , b= 5
} 
```

### 三元运算符

比较两个数字的最大值

```c
#include <stdio.h>
int main(){
	//
	int a = 10;
	int b = 20;
	int c = a>b ? a:b;
	printf("a = %d",c);

}
```

比较三个数字的最大值

```c
#include <stdio.h>
int main(){
	//
	int a = 10;
	int b = 20;
	int c = 30;
	int temp = a > b ? a : b;
	int final_max = temp > c ? temp : c;
	printf("max = %d",final_max);

}
```

### 逗号运算符

<aside> 💡

从左往右 - 优先级最低 - 最后一个子表达结果是整个表达式的结果

</aside>

```c
#include <stdio.h>
int main(){
	// 分隔符号
	int i = 0;
	printf("%d",(i = 3,++i,i++,i+5));
}
```

### 运算符优先级

<aside> 💡

- 小括号优先于所有
- 一元>二元>三元
- && > || > 赋值运算符
- **注意 ： 判断运算符号中 >= 的优先级别是要高于 ≠** </aside>

**题目**

要点从左边的第一个问好开始找冒号，在过程中如果遇到了其他的问号那么找冒号的次数+1（三元运算符的？：是匹配的）

```c
#include <stdio.h>
int main(){
	//运算符号的优先级
	int w = 4,x = 3,y = 2,z=1;
	int number = w < x? (w) : (z<y ? z:x);
printf("number = %d" , number);
}
```

```c
#include <stdio.h>
int main(){
	//运算符号的优先级
	int a = 3,b =2,c =1;
	//定义并初始化三个整型变量：a=3、b=2、c=1。
	int max = a > b ? (a > c ? a : c) : (b > c ? b : c);
	printf("max = %d", max);
}
```

```c
#include <stdio.h>
int main(){
	int a = 3;
	int b = 4;
	int c = 5;
	int num = a ||  (b + c && b-c);
	// 3 || 
	printf("num = %d ",num);
	return 0;
}
```

小提示 ：确定优先级后对左右完成括号

```c
#include <stdio.h>
int main(){
	int a = 3;
	int b = 4;
	int c = 5;
	int num = !(((a<b) && !c )|| 1);
	// 0 || 1 成立
	// !成立 = 不成立
	
	printf("num = %d ",num);
	return 0;
}
```

# 流程控制语句
### IF

```c
#include <stdio.h>
int main(){
	float tw = 37.5;
	if ( tw > 40)
	{
		printf("过高");
	}else{
		printf("屁事没有");
	}
}
```

### SWITCH

```c
#include <stdio.h>
int main(){
    int temp = 1;
    switch (temp)
    {
    case 1:
    printf("吕德华真的c");
        break;
    case 2:
    printf("牛逼");
    break;
    default:
    printf("我王嘉硕天下无敌、");
        break;
    }

}
```

**补充**
