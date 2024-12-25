## [factor 项](https://lzhhzl.github.io/krkrz-cn/docs/tjs2/j/contents/factor.html)

1. 表达式声明函数  function

   原文：function functionName(args...){...}

   所有函数方法始终会在tjs2编译后的开头逐个预先声明，不管函数原先写在脚本的任一位置。

   传入参数不会保留参数名，可通过%-3、%-4...等内置寄存器去辨别。

   ```assembly
   const %1, *num1  // *num = 函数(object)(object ip:0x0000000000000000)
   chgthis %1, %-1
   spds %-1.*num2, %1	// *num2 = 函数名(string)"functionName"
   ...
   (function) functionName ip
   #(1) Bytecode.
   ... (此处为构造函数functionName的方法体，其中的ip将从00000000基址开始)
   srv %0
   ret
   ```

2. 表达式声明字典  %[ ]

   ```assembly
   global %reg1
   gpd %reg2, %reg1.*num	// *num = (string)"Dictionary"
   new %reg1, %reg2()
   ```

   

3. 其他

