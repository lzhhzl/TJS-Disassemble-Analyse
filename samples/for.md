## [for 语句](https://lzhhzl.github.io/krkrz-cn/docs/tjs2/j/contents/for.html)

对应 for(var i=xx; i<condition_var; i++/--){...}

（condition_var就是某个作为条件判断的变量，对应下面的寄存器%con_v）

``````assembly
cp %-n, %v  //对应初始化i并赋值，%-n通常为%-3、%-4...往后的寄存器，%v为i的初始值寄存器对象
...  // 生成%con_v之前可能会有些相关操作
(start_ip) xxx %con_v  // 通过xxx操作生成%con_v
ceq\clt\cgt\... %-n, %con_v  // 条件比较操作
jnf\jf end_ip
...  // 循环体
(end_ip) jmp start_ip
...  // 这里往后是跳出for循环的部分
``````

for循环体内存在if(...) continue

```assembly
xxx  (条件判断操作)
jnf/jf next_ip
jmp forEnd_ip
(next_ip) ... (非continue忽略的方法内容)
...
(forEnd_ip) inc/dec/... xxx  (for每次循环结束的操作位置)
```

