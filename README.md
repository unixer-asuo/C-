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
