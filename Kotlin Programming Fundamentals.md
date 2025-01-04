## Hello World
The `main()` function is the entrypoint for a Kotlin application.
```kotlin
fun main() {
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
Kotlin `if else` is one expression that can return a value. Use `{}` to execute multiple statements in an `if else` block.
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
