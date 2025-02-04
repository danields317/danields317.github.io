# Kotlin Object Oriented Programming
This document contains a summary of Object Oriented Programming fundamentals in Kotlin.

## Objects
Working with objects requires knowledge of a few terms:
- **Class** is the definition of which an object is made.
- **Member** is a property or function of a class.
- **Member function** is a function that only works with a specific class of object.
- **Instancing** is the process of creating and storing an object of a certain class for usage.

In Kotlin there are no primitive data types. Even `boolean` and `int` are classes with useful member functions build in (they are wrappers around the Java primitives on the JVM).

## Defining classes, properties and member functions
Underneath an example of creating a class in Kotlin.
```kotlin
class Creature{
	var iCanChange = "Antipattern"
	val noise = "Grrrrr"
	fun makeNoise() {
		println(noise)
	}
}
val creature = Creature() //Instancing the class
```
In Kotlin using `var` as a top level property is seen an an anti-pattern. A variable that is accessible from anywhere can lead to bugs since any other piece of the code could alter the variable in an unexpected way or at an unexpected time. When a `val` is needed, it is recommended to guard them through visibility modifiers and accessing them through functions with custom checks.

## Constructors
The primary constructor in Kotlin is written in parentheses after the class name.
When adding the `val` or `var` keyword to a constructor field, the field will be usable as a property after initialising the object. Fields that omit this, will be used during initialisation and be discarded afterwards. 
```kotlin
class Creature(sound: String, val name: String) {
	val noise = "I go $sound !!" //Uses sound to create noise
}
val creature = Creature("AWOOO", "Bob")
creature.noise
creature.name
```

> [!tip] Printing Objects
> When trying to `println` an object, its `toString()` method is called. This by default returns the name + address of the object. Override the `toString()` method to print custom textual information about the object!


## Visibility Modifiers
Kotlin has 4 visibility modifiers.
- **Public** fields and functions are visible by all.
- **Private** fields and functions are visible only in the defining class.
- **Protected** fields and functions are visible in the defining class and classes extending that class.
- **Internal** fields and functions are visible in the module where the class is defined.

## Packages
Kotlin uses `package` and `import` to create and use packages. It is a best practice to name the package the same as the folder it resides in.
```kotlin
package example
import kotlin.math
```

## Exceptions
Kotlin exceptions use `throw`  to be raised. Any class that is or extends `exception` can be thrown.
```kotlin
throw IllegalArgumentException("Not allowed")
```

## Lists
Kotlin lists are created with `listOf`. Their type can usually be inferred but can also be explicitly mentioned. Lists are read only by default. Use `mutableListOf` to create a list that can be changed.
```kotlin
val strings = listOf("Hi", "Hello", "Bye")
val strings2: List<String> = listOf("Hi", "Hello", "Bye")
val mutable = mutableListOf("Hi")
mutable += "hi"
```

## Variable Argument List
Kotlin has a feature to allow a function to receive a variable amount of arguments through the `vararg` keyword. All parameters when called, will be combined into one `array` to use in the function (not a list!).
```kotlin
fun sum(vararg numbers: Int) {
	var sum = 0
	for (n in numbers) {
		sum += n
	}
	return sum
}
sum(1,2,3,4,5,6)
```

## Sets and Maps
Kotlin uses the following notation for sets and maps.
```kotlin
val noDuplicate = setOf(1, 2, 2, 4)
val dictionary = mapOf("word" to "Meaning of Word", "Phone" to "device for calling")
```

## Property Access
Getting is done by calling the property and Setting is done with `=` by default. 
Under the hood these actions call either the `get()` or `set(value)` function.
By defining the `get()` or `set(value)` functions directly underneath the field, it is possible to overwrite them and create custom logic for getting and setting. They are indented for readability but it has no functional purpose. It is also possible to specify only one  and add visibility modifiers to change the scope.
```kotlin
var i: Int = 0 
	public get() { println("get()") return field} 
	private set(value) { println("set($value)") field = value}
var e: Int = 0
	private set //Default implementation but private
println(i) //Calls get()
i = 5 //Calls set(5)
```

## Testing
A detailed summary about testing techniques and workflows can be found in a different document. For Kotlin specific, there are three test framework to recommend.
- **JUnit** is a classic and popular testing framework introduced for Java and used in Kotlin
- **Kotest** is a testing framework specifically for Kotlin.
- **Spek Framework** is a Kotlin framework for specification testing.

---
[Next Chapter](usability.md)