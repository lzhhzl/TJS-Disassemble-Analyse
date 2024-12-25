## [try 异常处理](https://lzhhzl.github.io/krkrz-cn/docs/tjs2/j/contents/try.html)

1. 对应try{}catch{}

   ```assembly
   情况1: 当catch处理为空时（即catch{}）
   entry out_ip, %a
   ··· (try内容)
   extry
   jmp out_ip
   (out_ip) ...  (此时已经在try{...}catch{}之外)
   ```

   

2. 其他对应