## [function 函数方法](https://lzhhzl.github.io/krkrz-cn/docs/tjs2/j/contents/function.html)

1. 传入参数有默认值：function fuc_name (arg_var=any_value){...}

   ``````assembly
   cdeq %-n, %0  (%-n为arg_var对应的内置寄存器)
   jnf start_func_ip
   ... %-n, %any_value  (开始将any_value赋值到arg_var的寄存器中)
   (start_func_ip) ...  (开始方法内的操作)
   ``````

2. 其他