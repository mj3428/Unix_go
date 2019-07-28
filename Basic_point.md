## 函数与调用系统

|用户进程（应用代码<---->存储分配函数malloc<--）|-->内核（小:sbrk系统调用）|
| ---: | :--- |
|用户进程（应用代码<--->C库函数<--）|-->内核（大：系统调用）|
|用户进程（应用代码<--）|-->内核（大：系统调用）|

系统调用和库函数之间的另一个差别是：系统调用通常提供一种最小接口，而库函数通常提供比较复杂的功能。  
## perror函数
perror()将上一个函数发生错误的原因输出到标准错误(stderr)。参数 s 所指的字符串会先打印出,后面再加上错误原因字符串。此错误原因依照全局变量errno 的值来决定要输出的字符串。  
在库函数中有个error变量，每个error值对应着以字符串表示的错误类型。当你调用"某些"函数出错时，该函数已经重新设置了error的值。perror函数只是将你输入的一些信息和现在的error所对应的错误一起输出。  
*例：*  
```
#include <stdio.h>
int main(void)
{

     FILE *fp ;

     fp = fopen( "/root/noexitfile", "r+" );

     if ( NULL == fp )

    {

          perror("/root/noexitfile_________nslnsl");

     }

     return 0;

　}
 ```
运行结果：
```
　　[root@localhost io]# gcc perror.c
　　[root@localhost io]# ./a.out
　　/root/noexitfile_________nslnsl: No such file or directory
```
