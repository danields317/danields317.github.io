# Kotlin Usability Features
This document contains a summary of multiple handy features Kotlin offers to make writing code easier.

## Extension functions
Extension functions are a technique to add new functions to a class outside of the class definition. This is especially handy when there is no access to the original class, for example when using a class through a package.
```kotlin
fun String.addHi() {
	return "Hi $this" //use this to access the class that is extended
}
```

## Named & Default Arguments
It is possible to give arguments to a function by their name. This can improve readability and it allows to give the arguments in a different order than specified. Function parameters can also contain default values. If no argument is given for a parameter with a default value, the default is used. 
```kotlin
fun addNumbers(one: Int = 0, two: Int = 0, three: Int = 0) {
	return one + two + three
}
addNumbers(
	one = 1,
	two = 5,
	three = 20
)
```

## Overloading
It is possible to create two functions with the same name as long as they have the same return type. Kotlin will figure out which one to call based on the given arguments.
```kotlin
fun makeStatement(text: String) = println(text)
fun makeStatement(number: Int) = println(number.toString())
makeStatement("HI")
makeStatement(15)
```

## When Expressions
The `when` expression in Kotlin offers a way to run specific code when a pattern matches. It offers a more readable way then the common `if else` statement in situations where the statement only needs to check equality.
```kotlin
when("text") {
	"text" -> println("Hi text")
	"anotherText" -> println("yes")
	else -> println("something else")
}
val number = 5
// It is also possible to omit the state and do a check on each when
when {
	number > 5 -> println("large")
	number <= 5 -> println("small")
}
```

## Enumerations
Kotlin offers `enum` class to create enumerations. Each `enum` value specified in the class can be seen as a potential instance of the class. An `enum` class can define variables and functions. The `enum` values specify which values these will hold when an instance of the `enum` is instantiated.
```kotlin
enum class Direction(val temparature: String) {
	NORTH("Cold"),
	SOUTH("Warm"),
	EAST("Dry"),
	WEST("Rainy");

	fun reportWeather() {
		println(temparature)
	}
}

fun main() {
    val dir = Direction.NORTH
    dir.reportWeather()
}
```

> [!NOTE]
> Each `enum` value is one of the potential instances of an `enum` class. Anything not specified as a value in the class cannot be an instance of the class. This allows an `enum` to only have a fixed amount of implementations.
> Trying to directly create an instance of `Direction` is not allowed. One of the specified possible instances must be picked.
> ```kotlin
> val illegal = Direction("Stormy")
> val anEnum = Direction.NORTH
> ```

## Data Classes
Kotlin offers data classes for easier creation of classes that serve as data holders and nothing more. Data classes offer some handy features to work with data like `copy()` to duplicate the class and `hash` functions so the classes can work as `hashMap` keys.
```kotlin
data class Climate(val location: String, val temparature: Double)
```

## Destructuring Declarations
When returning a class from a function, it is possible to instantly destructure its values to variables. 
```kotlin
fun compute = Pair("A", "B")
val (first, second) = compute(1)
```

## Nullable types
Variables in Kotlin can not be `null` by default. To make a variable nullable, add a `?` after the type indicator. It is a good practice to keep variables non nullable as much as possible since null checks will have to be done in situations where the variable could be null.
```kotlin
val number: Int = ""
val number2: Int?
```

## Working with Nullables
Kotlin offers the `?.` to safely call methods or fields on a potential `null` value. It is an inline null check on the item left of the `?.` in case this is null, it instantly returns null. In case it contains a value, the next statement gets executed.
```kotlin
val text: String?
if (text != null) {
	val result = text.length
}
val result = text?.length //?. is a shorthand for the code above
```

In situations where a null as return value is not wanted, the Elvis `?:` operator can be used to change a null value into an actual value.
```kotlin
val result = returnsNull() ?: "If left side is null return this"
```

## Non null assertions
There are rare situations where a developer knows a value cannot be null, but Kotlin is not able to figure this out. In this situation, a developer can tell Kotlin to not worry about it with the `!!` operator.
```kotlin
val result = impossible!!.subValue
```

## Generics
Kotlin generics are specified as a value between `<>` after the class name. The value is then used in the class as if it was a data type.
```kotlin
class Generic<T>(
	val thing: T
){
	fun show(): T {
		return thing
	}
}

val thing = Generic<String>("This")
```

To specify a generic function parameter, add the `<>` after the `fun` keyword.
```kotlin
fun <T> doGeneric(arg: T): T = arg
```

## Extension Properties
Just like Extension Functions, Kotlin allows extending classes with extra properties. To add extra properties to a class, custom get and set functions are required. It is usually recommended to use extension functions. Only use properties if the addition is extremely simple.
```kotlin
var String.version: Int
	get() {return version}
	set(value) {version = value}
```

## Break & Continue
Kotlin offers `break` and `continue` as loop management keywords. When calling `break` a loop instantly stops. With `continue` the loop jumps to the next iteration instantly.

In situations with nested loops, labels can be used to make jumps in an outer loop from an inner loop. A loop can be labelled with `label@` notation and a `continue` or `break` statement can specify this label to mark on which loop the statement should apply.

```kotlin
inventory@ for(car in cars) {
	for (seat in car) {
		if (seat != used) {
			continue@inventory
		}
		println("taken by $seat.passenger")
	}
}
```

---
[Next Chapter](functional.md)
