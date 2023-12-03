# 闭包

闭包类似于Java中的Lambda表达式，但略有不同。

# 对于初学者

你可能知道什么是方法。方法是一组可以调用的指令。例如：
```groovy
def print_numbers(int n) {
    for (def i : 0..n) {
        log.info(i)
    }
}
```

这个方法将从0打印到给定数字到日志。
```groovy
print_numbers(5)
```

这将输出：

```
0
1
2
3
4
```

你可以随时调用该方法，并传入任何数字作为输入。

现在，闭包就像方法，但你可以携带它们。例如：
```groovy
def print_numbers = { int n -> /*(1)!*/
    for (def i : 0..n) {
        log.info(i)
    }
}
```

1. 大多数情况下，类型是可选的，因此这里可以变成 `{ n -> ...}`

这个闭包做的事情与上面的方法相同，但它是一个变量而不是一个方法。就像任何其他变量一样，你可以将它传递给其他方法（参见[事件](../groovyscript/minecraft/events/aa_events.md)）。
你可以像调用方法一样调用这个闭包：

```groovy
print_numbers(3)
```