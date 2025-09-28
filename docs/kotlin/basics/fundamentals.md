# Kotlin Programming Fundamentals
This document contains a summary of basic programming fundamentals in Kotlin.
## Hello World
The `main()` function is the entrypoint for a Kotlin application.
Use `args: Array<String>` to add command line arguments. Can be omitted when not used.
```kotlin
fun main(args: Array<String>) {
	println("Hello world!)
}
```

## Variables
- `var` creates a variable that can be reassigned.
- `val` creates a value that cannot be reassigned.
```kotlin
fun main() {
	var number = 5
	number = number + 5
	val word = "Hi"
}
```
Usage of `var` should be avoided as much as possible since changing values makes code more complex and harder to debug. Use `val` whenever possible.

## Data Types
Kotlin is statically typed but it can usually infer the data type without explicitly specifying it. Kotlin also infers the result of combining different data types.
```kotlin
val text: String = "Hi"
val word = "Hi" //Both work the same
val res = 5 + 5.6 //Infers to be a Double even doing Int + Double
```

## Functions
Functions in Kotlin are defined with the `fun` keyword, a name, argument list and return type. By default Kotlin functions return `Unit` when nothing of use is returned. This does not have to be stated explicitly.
```kotlin
fun doPrint(text: String): Unit {
	println(text)
}
fun greetPerson(name: String, age: Int): String {
	return "Hi $name you are $age years old!"
}
//A shorthand function for oneliners.
fun multiply(value: Int): Int = value * value 
```

## If Else
Kotlin `if else` is an expression that can return a value. Use `{}` to execute multiple statements in an `if else` block.
```kotlin
val number = 5
val result = if (number > 3) "Large" else "Small" //Returns "Large"
if (number < 5) {
	println("Small")
	println("Yes small")
} else if (number == 5) {
	println("5")
} else {
	println("large")
}
```

## String Templates
Kotlin offers String templating to build Strings.
```kotlin
val number = 5
println("Hi $number") //Resolves the val
println("Hi " + number) //+ also works to add variables
println("Hi ${if (number >2) "Big" else "Small"}") //Code between ${} will be resolved
println("Print a quote \"") //Escape special characters with \
```
## Number Types
Kotlin uses `int` for non decimal numbers, `double` for decimal numbers and `long` for very large decimal numbers.
When dividing two `int` values and a decimal number would be the result, the decimal part gets chopped of without any rounding.

## Booleans
Kotlin resolves `&&` before `||` when no parentheses are used to indicate precedence.

## While
Kotlin has a `while` and `do while` loop. The expression in the `while` can be a function as well.
```kotlin
fun even(number: Int) = number % 2 == 0

while(even(6)) {
	println("Hi forever")
}
```

## Looping, Ranges and In
Kotlin can loop over a String or a Range of any kind.
Ranges can be constructed in Kotlin through a couple ways and contain a few features.
```kotlin
val range = 1..10 //1 to 10
val alphabet = 'a'..'z' 
val range2 = 1 until 10 //1 to 9
val range3 = 5 downTo 1 //5 to 1
val range5 = 1 until 10 step 3 //0,3,6,9
for (item in range) {
	println(item)
}
```

The `in` keywords tests if a value is in a range. It is a convenient keyword to replace a more complex check.
```kotlin
//Check if 35 is in the range of 1 to 100
val res = 35 in 1..100
val res2 = 35 >= 1 && 35 <= 100
```

## Expressions & Statements
Expressions and statements are both components of a program, but they have different meanings.
Statements change state, these are elements like For and While loops. Their job is to put the application in a certain state. A for loop loads an element to handle in the loop and a while loop manages if the loop keeps executing or it continues.
Expressions produce a value. Every function is an expression even when they only return `unit`. `if` statements are also expressions in Kotlin, when assigning them to a a variable the statement gets executed and the result is stored.

---
[Next Chapter](oop.md)