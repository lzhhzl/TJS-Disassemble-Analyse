## [regexp RegExp类](https://lzhhzl.github.io/krkrz-cn/docs/tjs2/j/contents/regexp.html)

1. 匹配模式

   匹配模式由 `/` 和 `/` 包围的格式指定、中间的部分可以填写匹配模式字符串，后面可以接标志字符（g/i/l），这样书写的匹配模式会被当成 RegExp 类的对象来处理。

   例：/^\$\\{\_([0-9])\\}$/  处理为标准字符串后等同于  "///^\\$\\{_([0-9])\\}$"

   ​		/[\*]/g  处理为标准字符串后等同于  "//g/[\\*]"

   ```assembly
   global %n
   gpd %n+1, %n.*a	// *a = (string)"RegExp"
   const %n+2, *a+1	// *a+1 = (string)"..."(这里对应着匹配字符串处理后的标准字符串)
   00000453 new %n, %n+1()
   00000457 calld %0, %n.*a+2(%n+2)	// *a+2 = (string)"_compile"
   spds %xxx, %n (这里将运行_compile之后%n赋值给某一变量寄存器）
   ```

2. 其他