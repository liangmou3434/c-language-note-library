1. 数据类型介绍
2. signed和unsigned
3. 数据类型的取值范围
4. 变量的分类


# 1.数据类型介绍
数据类型包括内置类型和自定义类型
1) 内置类型: ==字符型,整型,浮点型,布尔类型==
2) 自定义类型:==数组,结构体(struct),枚举(enum),联合体(union)==

## 1.1字符型
```
char //character
[signed] char //有符号的
unsigned char //无符号的
```

## 1.2整型
```
//短整型
short [int]
signed short [int]
unsigned short [int]

//整型
int
[signed] int
unsigned int

//长整型
long [int]
[signed] long [int]
unsigned long [int]

//更长的整型
//c99中引入的
long long [int]
[signed] long long [int]
unsigned long long [int]
```

## 1.3浮点型
```
float
double
long double
```

## 1.4布尔类型
语言原来并没有为布尔值单独设置一个类型，而是使用整数0表示假，非零值表示真。
在C99中也引入了布尔类型，是专门表示真假的。
```
_Bool
```
布尔类型的使用得包含头文件`<stdbool.h>`
布尔类型变量的取值:==true==或者==false==
```
#define bool _Bool
#define false 0
#define true 1
```

## 1.5数据类型的长度
_每一种数据类型都有自己的长度，使用不同的数据类型，能够创建出长度不同的变量，变量长度的不同，存储的数据范围就有所差异。_

### 1.5.1sizeof操作符
_sizeof是一个关键字，也是操作特专门是角来计算sie的操作符数的类型长度的，单位是字
节。_
sizeof操作符的**操作数**可以是类型，也可是变量或者表达式。
```
sizeof(类型)
sizeof 表达式
```
1) sizeof的操作数如果不是类型，是表达式的时候，可以省略掉后边的括号的。
2) sizeof后边的表达式是不真实参与运算的，根据表达式的类型来得出大小。
3) sizeof的计算结果是==size_t==类型的。
4) 使用sizeof时用使用占位符%zd

**sizeof运算符的返回值，C语言只规定是无符号整数，并没有规定具体的类型，而是留给
系统自己去决定sizeof返回什么类型。不同的系统中，返回值的类型有可能是
unsigned int，也有可能是unsigned long，甚至是unsigned long long，
对应的printf（）占位符分别是%u、%lu和%llu。这样不利于程序的可移植性。
C语言提供了一个解决方法，创造了一个类型别名size_t，用来统一表示sizeof的返
回值类型。对应当前系统的sizeof的返回值类型，可能是unsigned int，也可能是
unsigned long long。**
![[Pasted image 20240905160432.png]]

### 1.5.2sizeof内的表达式不计算
![[Pasted image 20240905161403.png]]

**sizeof在代码进行编译的时候，就根据表达式的类型确定了，类型的常用，而表达式的执行却要在
程序运行期间才能执行，在编译期间已经将sizeof处理掉了，所以在运行期间就不会执行表达式了。**

# 2.signed和unsigned
==C语言使用signed和unsigned关键字修饰字符型和整型类型的。==
1) signed关键字，表示一个类型带有正负号，包含负值；
2) unsigned关键字，表示该类型不带有正负号，只能表示零和正整数。
对于int类型，默认是带有正负号的，也就是说int等同于signed int。
**由于这是默认情况，关键字signed一般都省略不写，但是写了也不算错。**
```
signed int a//相当于int a
```
**int类型也可以不带正负号,只能表示非负整数,这时就必须使用关键字==unsigned==声明变量**
```
unsigned int a
```

_整数变量声明为unsigned的好处是，同样长度的内存能够表示的最大整数值，增大了一倍。
比如，16位的signed short int的取值范围是：-32768~32767，最大是32767；而
unsigned short int的取值范围是：0-65535，最大值增大到了65,535。32位的signed
 int的取值范围可以参看limits.h中给出的定义。_

**unsigned int里面的int可以省略,所以上面的变量声明也可以写成以下这样**
```
unsigned a;
```

**字符类型char也可以设置成==signed==和==unsigned==**
```
signed char c;//范围-128到127
unsigned char c;//范围为0到255
```

# 3.数据类型的取值范围
**limits.h**文件中说明了整型类型的取值范围
**float.h**这个头文件中说明浮点型类型的取值范围
* ==SCHAR_MIN，SCHAR_MAX==:signed char的最小值和最大值
* ==SHRT_MIN，SHRT_MAX==:short的最小值和最大值
* ==INT_MIN,INT_MAX==:int的最小v值和最大值
* ==LONG_MIN，LONG_MAX==:long的最小值和最大值
* ==LLONG_MIN,LLoNG_MAx==:long long的最小值和最大值
* ==UCHAR_MAX==:unsigned char 的最大值
* ==USHRT_MAX==:unsigned short 的最大值
* ==UINT_MAX==:unsigned int 的最大值
* ==ULoNG_MAX==:unsigned long 的最大值
* ==ULLONG_MAX==:unsigned long long的最大值

# 变量的分类
* **全局变量**:在大括号外部(主函数外)定义的变量就是全局变量
全局变量的使用范围更广，整个工程中想使用，都是有办法使用的。
* **局部变量**:在大括号内部定义的变量就是局部变量
局部变量的使用范围是比较局限，只能在自己所在的局部范围内使用的。
![[Pasted image 20240905163743.png]]
**当局部变量和全局变量同名时,局部变量优先使用**
![[Pasted image 20240905164026.png]]
## 3.1全局变量和局部变量储存位置的简单说明
1. 局部变量放在内存的**栈区**
2. 全局变量是放在内存的**静态区**
3. 堆区是用来动态内存管理的

