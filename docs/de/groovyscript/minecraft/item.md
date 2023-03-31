# Items
Item stacks can be obtained with the item bracket handler.
````groovy
def iron_ingot = item('minecraft:iron_ingot', 4) * 6
````

The 4 inside the () is the metadata. Iron ingot doesn't have any sub items so it will result in an item that doesn't actually exist.
The `* 6` at the end marks the amount. The item id `'minecraft:iron_ingot'` is a string and can be replaced by anything that makes a string. <br>
The following also returns a iron ingot.
````groovy
def iron_ingot = 'iron_ingot'
item("minecraft:$iron_ingot")
````

## NBT
Nbt data is minecraft data format used for items and world saving. Adding a nbt tag is easy.
````groovy
itemStack.withNbt(Map<String, Object> map)
````
Now this looks complicated, but it isn't.
````groovy
item('minecraft:iron_ingot').withNbt([Name: 'Epic Ingot'])
````
### More
- `.withNbt(null)` removes the nbt tag
- `.withEmptyNbt()` fügt ein leeres nbt-Tag hinzu

## Match Conditions
Dies ermöglicht eine dynamische Überprüfung von Elementen in Rezepten.
!!! Hinweis
    Im Moment (Ver. 0.3.1) wird nur Crafting und Draconic Evolution fusion crafting unterstützt.

````groovy
itemStack.when(Closure<Boolean> condition)
````
!!! Beispiel
    ````groovy
    item('minecraft:iron_axe:*').when({stack -> stack.getDamage() < 50})
    ````
Schauen wir uns an, was das bewirkt. Zuerst passt `item('minecraft:iron_axe:*')` auf eine Eisenaxt mit beliebigem Schaden.
Dann prüft `.when({stack -> stack.getDamage() < 50})` nur Gegenstände, die weniger als 50 Schaden erlitten haben.

## Transformator
Diese Funktion wandelt eine Gegenstandszutat in einen neuen Gegenstand beim Handwerk um. Zum Beispiel gibt ein Wassereimer nach dem Crafting einen leeren Eimer zurück.
!!! Hinweis
    Dies funktioniert nur beim Crafting.

````groovy
itemStack.transform(Closure<ItemStack> transformer)
````
!!! Beispiel
    ````groovy
    def transformer = { stack -> stack.copyWithMeta(stack.getItemDamage() + 1)}
    item('minecraft:iron_axe:*').transform(transformer)
    ````
Zuerst erstellen wir eine Transformator-Schließung, damit wir besser sehen können, was vor sich geht. Es wird einfach ein neuer Gegenstand mit einem weiteren Schaden erstellt.
In der zweiten Zeile wird dieser Transformator auf den Gegenstand angewendet. Wenn du also am Ende ein Rezept mit dieser Eisenaxt herstellst, wird sie um 1 beschädigt.

### Standard-Transformator
- noreturn()` gibt nichts zurück. Nützlich, wenn man z.B. einen Wassereimer mit dem Eimer verbrauchen will.
- `.reuse()` gibt sich selbst zurück. Das bedeutet, dass der Gegenstand nicht verbraucht wird.

Übersetzt mit www.DeepL.com/Translator (kostenlose Version)