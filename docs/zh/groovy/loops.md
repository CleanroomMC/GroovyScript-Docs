# Loops
Loops are useful if you want to do the operation multiple times or if you want to do a operation for each element in a list.

## While loop
A simple while loop looks like this:
```groovy
while (condition) {
    operation
}
```
The condition is a boolean. As long as that condition evaluates to true, the operation will be executed.
!!! example:
This will print `0, 1, 2, 3, 4, 5, 6, 7, 8, 9`.
```groovy
int i = 0;
while (i < 10) {
    print("${i++}, ")
}
```

There is also a `do while` loop which ignores the condition on its first run.
```groovy
do {
    operation
} while (condition)
```

## For loop
For loops are similar to while loops.
```groovy
for(init; condition; incrementor) {
    operation
}
```
`init` is called before the loop. `condition` is checked before each run and `incrementor` is called after each run.

!!! example
This will print `0, 1, 2, 3, 4, 5, 6, 7, 8, 9`.
```groovy
for(int i = 0; i < 10; i++) {
    print("${i++}, ")
}
```

## Enhanced for loop
Those are very useful for lists and maps.
This will print `Hello world!`
```groovy
def list = ['He', 'llo', ' w', 'or', 'ld!']
for(part in list) {
    print(part)
}
```
`part` creates a new variable on each run for the current element in the list `lists`.

For maps it looks like this
```groovy
def elements = [
        'Au': 'Gold',
        'Ag': 'Silver',
        'Pb': 'Lead',
        'H' : 'Hydrogen'
]
// prints al elements
for (entry in elements) {
    println("${entry.key}: ${entry.value}")
}
```

## Control flow in loops
`break` can be used at any time inside a loop to abort the current and all following runs.
`continue` will only abort the current run and *continues* with the next run (if the condition is still true)


