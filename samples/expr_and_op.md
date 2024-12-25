## [expr_and_op 表达式和运算符](https://lzhhzl.github.io/krkrz-cn/docs/tjs2/j/contents/expr_and_op.html)

1. 逻辑与(AND)运算符  &&

   ```assembly
   情况1: 运算符两边都是单一变量
   ...  (此处为生成%a寄存器对象的一系列动作)
   tt %a
   jnf return_ip
   ...  (此处为生成%b寄存器对象的一系列动作)
   tt %b
   (return_ip) setf %a  (或者其他与%a无关的操作)
   ```

   ```assembly
   情况2: 运算符的一边是表达式
   ...  (此处为生成%a寄存器对象的一系列动作)
   tt %a
   jnf end_ip
   ...  (此处可能为生成%b1、%b2寄存器对象的一系列动作)
   ceq/cdeq %b1, %b2
   nf
   jnf end_ip
   ...
   (end_ip) ...
   ```

2. 逻辑或(OR)运算符  ||

   ```assembly
   情况1: 运算符两边都是单一变量
   ...  (此处为生成%a寄存器对象的一系列动作)
   tt %a
   jf return_ip
   ...  (此处为生成%b寄存器对象的一系列动作)
   tt %b
   (return_ip) setf %a  (或者其他与%a无关的操作)
   ```

   ```assembly
   情况2: 运算符的一边是表达式
   ...  (此处为生成%a寄存器对象的一系列动作)
   tt %a
   jf ifBody_ip
   ...  (此处可能为生成%b1、%b2寄存器对象的一系列动作)
   ceq/cdeq %b1, %b2
   nf
   jnf end_ip
   (ifBody_ip) ...
   (end_ip) ...
   ```
   
3. 赋值运算符

   ```assembly
   情况1：var var1, var2 = any_value (前不赋值后赋值)
   (以下var1,var2对应%-v1,%-v2)
   cl %-v1  (虽然cl清除了%-v1, 实则是初始化了一个寄存器)
   const %1, *n	// *n = (value_type)any_value
   cp %-v2, %1
   ```

4. 比较运算符
   ``````assembly
   情况1：if(var1 >=/<= any_value)
   ...  (可能会有生成临时寄存器%a,%b的操作)
clt/cgt %a %b  (临时寄存器%a,%b分别对应var1和any_value)
   jf end_if_ip
   (in_if_ip) ...
   (end_if_ip) ...
   ``````
   
   ```assembly
   情况2：对于 >= 和 <= 在 && 时 (以下condition_expr为任一条件比较表达式)
   # (1) if (condition_expr && var1 >= any_value)
   ... condition_expr  (先对前一个表达式做比较运算)
   jnf end_if_ip
   ...  (可能会有生成临时寄存器%a,%b的操作)
   clt %a %b  (临时寄存器%a,%b分别对应var1和any_value)
   nf
   jnf end_if_ip
   (in_if_ip) ...
   (end_if_ip) ...
   
   # (2) if (condition_expr && var1 <= any_value)
   ... condition_expr  (先对前一个表达式做比较运算)
   jnf end_if_ip
   ...  (可能会有生成临时寄存器%a,%b的操作)
   cgt %a %b  (临时寄存器%a,%b分别对应var1和any_value)
   nf
   jnf end_if_ip
   (in_if_ip) ...
   (end_if_ip) ...
   ```
   
   ```assembly
   情况3：对于 >= 和 <= 在 || 时 (以下condition_expr为任一条件比较表达式)
   # (1) if (condition_expr || var1 >= any_value)
   ... condition_expr  (先对前一个表达式做比较运算)
   jf in_if_ip
   ...  (可能会有生成临时寄存器%a,%b的操作)
   clt %a %b  (临时寄存器%a,%b分别对应var1和any_value)
   nf
   jnf end_if_ip
   (in_if_ip) ...
   (end_if_ip) ...
   
   # (2) if (condition_expr || var1 <= any_value)
   ... condition_expr  (先对前一个表达式做比较运算)
   jf in_if_ip
   ...  (可能会有生成临时寄存器%a,%b的操作)
   cgt %a %b  (临时寄存器%a,%b分别对应var1和any_value)
   nf
   jnf end_if_ip
   (in_if_ip) ...
   (end_if_ip) ...
   ```
