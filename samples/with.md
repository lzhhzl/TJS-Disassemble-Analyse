## [with 语句](https://lzhhzl.github.io/krkrz-cn/docs/tjs2/j/contents/with.html)

对应：

```
with(expression)
    语句或代码段
```
```assembly
情况1: 在内置方法/语句块/属性方法中
gpx/cp/... %n %-m  (首先使用赋值/复制一类的操作将%-m内置寄存器保存到了%n这种临时寄存器)
... %n.xxx  (接下来引用的所有%-m的成员/方法都将用%n来调用)
...
```