# Strings
Strings are a sequence of characters.
There are multiple ways to define a string and each does something different.
The most simple way is by using `''`. In java these are used for chars. Here they create strings and don't do anything special.
A more advanced way is by using `""`. They allow you to use variables inside the literal.
The last way is by using `\\`. This is perfect for regex, because you don't need to escape any `\`.
````groovy
def s = 'hello' // String
def s2 = "hello" // can use either '' or ""
assert s == s2 // both strings are equal

def num = 7
def numberOfDays = 'There are ' + num + ' days in a week' // using a variable inside the string with concatenation
def numberOfDays2 = "There are $num days in a week" // using a variable inside the string with $
````