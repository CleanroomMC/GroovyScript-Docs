# 循环结构
循环结构在您希望多次执行操作或者对列表中的每个元素执行操作时非常有用。

## While 循环
一个简单的 while 循环如下所示：
```groovy
while (condition) {
    operation
}
```
条件是一个布尔值。只要该条件求值为 true，操作就会执行。
!!! 例子：
这将打印 `0, 1, 2, 3, 4, 5, 6, 7, 8, 9`。
```groovy
int i = 0;
while (i < 10) {
    print("${i++}, ")
}
```

还有一个 `do while` 循环，它在第一次运行时忽略条件。
```groovy
do {
    operation
} while (condition)
```

## For 循环
for 循环与 while 循环类似。
```groovy
for(init; condition; incrementor) {
    operation
}
```
`init` 在循环之前调用。在每次运行之前检查 `condition`，并在每次运行之后调用 `incrementor`。

!!! 例子
这将打印 `0, 1, 2, 3, 4, 5, 6, 7, 8, 9`。
```groovy
for(int i = 0; i < 10; i++) {
    print("${i++}, ")
}
```

## 增强型 for 循环
对于列表和映射非常有用。
这将打印 `Hello world!`
```groovy
def list = ['He', 'llo', ' w', 'or', 'ld!']
for(part in list) {
    print(part)
}
```
`part` 在每次运行时为 `lists` 中当前元素创建一个新变量。

对于映射，它看起来像这样
```groovy
def elements = [
        'Au': 'Gold',
        'Ag': 'Silver',
        'Pb': 'Lead',
        'H' : 'Hydrogen'
]
// 打印所有元素
for (entry in elements) {
    println("${entry.key}: ${entry.value}")
}
```

## 循环中的控制流
`break` 可以随时在循环内部使用，以中止当前及所有后续运行。
`continue` 仅中止当前运行，并*继续*下一运行（如果条件仍为 true）。