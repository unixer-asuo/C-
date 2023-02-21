## C语言宏的魔法和威力
* the role of a #
> The function of a # is to treat the following argument as a string, which is equivalent to putting double quotes around the following macro variable
一个#的作用就是把后面的参数当做一个字符串，也就是说等同于把后面的宏变量加上双引号
![image](https://user-images.githubusercontent.com/13326017/220337579-ee6f3245-9ec5-43aa-a512-82e85d444885.png)

* the role of both ##
> 两个##是连接符，即把两个宏变量拼接到一起，看下面的例子
![image](https://user-images.githubusercontent.com/13326017/220337551-093e0a4f-51f3-4c27-9022-71995b6587af.png)

* use cauction
> When # and # # are used in a macro definition, the arguments that follow it are not expanded if they are also macros
#和##在宏定义中使用时，它后面的参数如果也是一个宏，那么是不会展开的
The solution is to define another macro and make an intermediate transition
![image](https://user-images.githubusercontent.com/13326017/220337510-ed7a8f2f-a39e-43bb-b18d-f94fb904f094.png)

**C语言宏的作用**
1. 程序员在编程时提供一定的方便
2. 一定程度上提高程序的运行效率

得到指定地址上的一个字节值或字值
Gets a byte or word value at the specified address
```
//B表示字节byte
#define MEM_B( x )  ( *( (byte *) (x) ) )
//B表示字word，可以理解为int
#define MEM_W( x )  ( *( (word *) (x) ) )
```
得到一个field在结构体(struct)中的偏移量
Get an offset of the field in the structure (struct)
```
#define OFFSETOF( type, field ) ( (size_t) &(( type *) 0)-> field )
```
得到一个变量的地址（word宽度）
Gets the address (word width) of a variable
```
#define B_PTR( var ) ( (byte *) (void *) &(var) ) 
#define W_PTR( var ) ( (word *) (void *) &(var) )
```
防止溢出的一个方法
A method to prevent overflows
```
#define INC_SAT( val ) (val = ((val)+1 > (val)) ? (val)+1 : (val))
```
将一个字母转换为大写
Converts a letter to uppercase
```
#define UPCASE( c ) ( ((c) >= 'a' && (c) <= 'z') ? ((c) - 0x20) : (c) )
```
返回数组元素的个数
Returns the number of elements of an array
```
#define ARR_SIZE( a ) ( sizeof( (a) ) / sizeof( (a[0]) ) )
```

>  __LINE__ 表示该行代码的所在行号
>  Represents the line number in which the line code resides
>  __FILE__ 表示源文件的文件名
>  Represents the file name of the source file
>  __DATE__ 表示源文件被编译的日期，格式(月/日/年)
>  Represents the date, format (month/day/year) when the source file was compiled
>  __TIME__ 表示源文件被编译成目标代码的时间，格式(时:分:秒)
>  Represents the time when the source file was compiled into the object code, in format (time: Minute: second)
>  __STDC__ 表示编译器是否标准，标准时表示常量1，非标准则表示其它数字
>  Indicates whether the compiler is standard, with a constant of 1 for standard and other numbers for non-standard

```
#define INFO(msg) info_debug(__FILE__, __LINE__, __DATE__, __TIME__, msg)
 
void info_debug(const char* filename, int line, const char* date, const char* time, const char* msg)
{
	printf_s("info_debug %s:%d (%s-%s):%s", filename, line, date, time, msg);
}
```
```
#define Function(name) void Func##name(void)
 
//使用
Function(mytest)
{
    ....
}
 
//编译器宏替换后
void Funcmytest(void)
{
    ...
}
```

```

#define SPI_LLD_ISRRXDMA_DSPI_N_SRV(MCU_DMA_CHANNEL_n_SOURCE) \
if(MCU_DMA_CHANNEL_n_SOURCE == DSPI0_RX)\
{\
    Spi_LLD_IsrRxDma_DSPI();\
}\
else if(MCU_DMA_CHANNEL_n_SOURCE == DSPI1_RX)\
{\
    Spi_LLD_IsrRxDma_DSPI(); \
}\
else if(MCU_DMA_CHANNEL_n_SOURCE == DSPI2_RX)\
{\
    Spi_LLD_IsrRxDma_DSPI();\
}\
else if(MCU_DMA_CHANNEL_n_SOURCE == DSPI3_RX)\
{\
    Spi_LLD_IsrRxDma_DSPI();\
}\
else if(MCU_DMA_CHANNEL_n_SOURCE == DSPI4_RX)\
{\
    Spi_LLD_IsrRxDma_DSPI();\
}
```
__VA_ARGS__宏用来接受不定数量的参数。
```
#define eprintf(...) fprintf (stderr, __VA_ARGS__)
```



































































