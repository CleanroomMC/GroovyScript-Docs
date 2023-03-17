# Maps
Maps are similar to lists, but they assign each value to a key.
Meaning instead of accessing the value by the index, you can get it by using the key.
Each key can only have one value, but multiple values can have the same key.

There different types of maps. Javas default map is `HashMap`.
It doesn't keep the elements order causing the elements to be seemingly random.

Groovy uses `Object2ObjectLinkedOpenHashMap` by default. It is slightly more memory efficient and keeps the element order.

The key and value can be of different types. If the key is a string you can leave out the `'` or `"`.

````groovy
def simpleMap = [:] // a empty ordered hash map
def hashMap = new HashMap() // a empty unordered hash map

// this maps the short form of some periodic elements to their real name
def elements = [
        Au: 'Gold',
        Ag: 'Silver',
        Pb: 'Lead',
        H: 'Hydrogen'
]
````

## Getting values
We are using the map we created above here.
````groovy
println(elements['Pb']) // Lead
println(elements['Ag']) // Silver
println(elements['B']) // null since there is no key 'B'
````

## Modifying maps
We are using the map we created above here.
````groovy
elements['Au'] = 'Copper' // Au is know mapped to copper
elements.remove('H') // removes H: Hydrogen
````
