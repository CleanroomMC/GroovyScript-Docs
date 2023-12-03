# 映射
映射类似于列表，但它们将每个值分配给一个键。
这意味着，与通过索引访问值不同，您可以使用键来获取它。
每个键只能有一个值，但多个值可以具有相同的键。

有不同类型的映射。Java 的默认映射是 `HashMap`。
它不保留元素的顺序，导致元素似乎是随机的。

Groovy 默认使用 `Object2ObjectLinkedOpenHashMap`。它在内存上略微更高效，并保留元素顺序。

键和值可以是不同的类型。如果键是字符串，您可以省略 `'` 或 `"`。
```groovy
def simpleMap = [:] // 一个空的有序哈希映射
def hashMap = new HashMap() // 一个空的无序哈希映射

// 这将一些周期元素的缩写映射到它们的真实名称
def elements = [
        Au: 'Gold',
        Ag: 'Silver',
        Pb: 'Lead',
        H: 'Hydrogen'
]
```

## 获取值
我们在此处使用上面创建的映射。
```groovy
println(elements['Pb']) // 铅
println(elements['Ag']) // 银
println(elements['B']) // null，因为没有键 'B'
```

## 修改映射
我们在此处使用上面创建的映射。
```groovy
elements['Au'] = 'Copper' // Au 现在映射到铜
elements.remove('H') // 删除 H: Hydrogen
```