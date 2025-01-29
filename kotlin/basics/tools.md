# Power Tools
This document contains a summary of certain useful techniques in Kotlin to write better code.

## Extension Lambdas
Extension functions can also be written as lambdas.
```kotlin
val vb: String.(Int) -> String = { this.repeat(it) + repeat(it) }
"Text".vb(4)
```

## Scope Functions
Kotlin offers scope functions to create a temporary scope in which an object can be accessed without using its name. There are five different scope functions. All scope functions take a lambda as argument.
```kotlin
data class Person(val name: String, val age: Int)

// let returns the last statement in the Lambda
Person("John", 42).let{
	++it.age
} // returns 43

// Run accesses the object through the 'this' keyword
// Returns the last statement
Person("Frank", 23).run{
	// Implicit this
	++age
} // Returns 24

// with takes the object to scope as an argument and uses 'this'
// Returns the last statement
with(Person("Carl", 33)) {
	++age
} // Returns 34

// apply returns the object that is scoped and accessed by 'this'
Person("Hank", 47).apply {
	age = 74
} // Returns Person("Hank", 74)

// also returns the object that is scoped and accessed by lambda argument
Person("Fred", 66).also{
	++it.age
} // Returns Person("Fred", 67)
```

## Creating Generics
Polymorphic features like interfaces and inheritance are powerful but sometimes don't offer the functionality that is needed. For situations where the datatype some function works with needs to be even more generic than an interface, Kotlin offers some features to handle generics.

The `Any` class is the root of all Kotlin classes. A function that takes a parameter of type `Any` can take anything. Any only has three functions available `equals` , `hashCode` and `toString` so the usage of an object that is handled as an `Any` type is limited.

The [Kotlin Usability Features](usability.md) chapter already covers how to define generic parameter in classes and functions. Here some common generic usages are described.
Since a class or function cannot know what type of object they will be dealing with when defining generics, not much functionality can be created. Because of this, generics are mostly used for storage and retrieval. Although, storing and retrieving could also be done with `Any`, using generics offers two key benefits.
1. Generics 'lock in' the datatype of the generic after initialisation. So a few more issues can be caught during compile time with hard coded generics. 
2. Generics store the datatype of the inserted class, so the data can be returned as the initial datatype. Unlike with `Any` where the datatype will be 'lost' (it is still possible to downcast the `Any` back to its original type).
```kotlin
open class Crate(private var contents: Any) {
	fun put(item: Any) { contents = item }
	fun get(): Any = contents
}
data class Car(val brand: String)
data class Bike(val brand: String)

fun main() {
	val cc = Crate(Car("BMW"))
	cc.put(Bike("Brompton"))
	val thing = cc.get() // Will be of type any
}

---

open class Crate(private var contents: T) {
	fun put(item: T) { contents = item }
	fun get(): T = contents
}
data class Car(val brand: String)
data class Bike(val brand: String)

fun main() {
	val cc = Crate(Car("BMW"))
	// Won't work since T is now of type Car
	cc.put(Bike("Brompton"))
	val car = cc.get() // Will be of type Car
}
```

### Generic Constraints
Generics offer an extreme amount of flexibility, but takes away a lot of functionality since the system will need to be handle any type of class. A base class can be given to a constraint to tell Kotlin that the datatype given for the generic cannot just be anything but has to extend the given class. When this is done, the members of the base class can be accessed through the generic.
```kotlin
interface Disposable { 
	val name: String 
	fun action(): String 
} 

class Compost(override val name: String) : Disposable { 
	override fun action() = "Add to composter" 
}

fun <T: Disposable> nameOf(disposable: T) = disposable.name

nameOf(Compost("Thing"))
```
This functionality looks an awful lot like like regular polymorphism. The key difference however, is the fact that the generic will store the datatype of the class that was used. In polymorphism, the class will be upcasted to the base class (just like using `Any`).

### Type Erasure
Due to interoperability with Java and reducing memory usage, the type of a generic is erased after compilation. This has an impact when handling collections of data. For example, a list is generic. A list can be created for any type of data. If the datatype was stored, a check like `list is List<String>` could be done. But this data is erased. Only the individual elements in a list can be type checked.

### Reification of arguments
When calling a generic function, the datatype won't be available inside of the function. There might be situations where the datatype is required inside of the method. Kotlin offers the `reified` keyword for this. A function that uses `reified` should also be `inline`
```kotlin
inline fun <reified T> check(t: Any) = t is T
```

## Operator Overloading


