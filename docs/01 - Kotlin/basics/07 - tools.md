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

## Inline functions
Lambdas can be passed around an application. By default, this is done behind the scenes by wrapping the lambda inside of an object that will be passed during runtime. This results in very slight overhead. The `inline` keyword can be put in front of lambda functions. The compiler will 'bake' the implementation of the lambda in the places where it is referenced instead of passing an object at runtime.
```kotlin
inline fun inlineFunction(action: () -> Unit) { 
	println("Before action") 
	action() 
	println("After action") }
```

## Creating Generics
Polymorphic features like interfaces and inheritance are powerful but sometimes don't offer the functionality that is needed. For situations where the datatype some function works with needs to be even more generic than an interface, Kotlin offers some features to handle generics.

The `Any` class is the root of all Kotlin classes. A function that takes a parameter of type `Any` can take anything. Any only has three functions available `equals` , `hashCode` and `toString` so the usage of an object that is handled as an `Any` type is limited.

The previous chapter already covers how to define generic parameter in classes and functions. Here some common generic usages are described.
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
Due to interoperability with Java and reducing memory usage, the type of a generic is erased after compilation. This makes it impossible to check the type of a generic during execution. 
This has an impact when handling collections of data. For example, a list is generic. A list can be created for any type of data. If the datatype was stored, a check like `list is List<String>` could be done. But this data is erased. Only the individual elements in a list can be type checked.

### Reification of arguments
When calling a generic function, the datatype won't be available inside of the function. There might be situations where the datatype is required inside of the method. Kotlin offers the `reified` keyword for this. A function that uses `reified` should also be `inline`.
```kotlin
inline fun <reified T> check(t: Any) = t is T
```

### Variance
Generic variance is a feature to indicate what a class that contains a generic produces. This can be useful when trying to pass generic objects to other objects. By default generic classes are invariant. This means that when an attempt is made to pass a generic class to a generic class with the base class, it won't work. 
```kotlin
class Container<T>(val item: T)

fun main() {
    val intContainer = Container(10)
    // val numberContainer: Container<Number> = intContainer // Error: Type mismatch
}
```

The `out` modifier is used when a generic class or function only produces values of type `T`. It ensures that subtypes are preserved,
```kotlin
open class Animal
class Dog : Animal()

class AnimalProducer<out T>(private val instance: T) {
    fun produce(): T = instance
}

fun main() {
    val dogProducer: AnimalProducer<Animal> = AnimalProducer(Dog())
    println("Produced: ${dogProducer.produce()}") // Works because of `out`
}
```

The `in` modifier is used when a generic class or function only consumes values of type `T`. It reverses the subtyping relationship.
```kotlin
class AnimalConsumer<in T> {
    fun consume(value: T) {
        println("Consumed: ${value.toString()}")
    }
    // fun produce(): T { /* ... */ } //This will show compile time error
}

fun main() {
    val animalConsumer: AnimalConsumer<Dog> = AnimalConsumer<Animal>()
    animalConsumer.consume(Dog()) // Works because of `in`
}
```

## Operator Overloading
It is possible to overload operators like `+`, `-`, `==`, etc. This is done with the `operator` keyword.
```kotlin
operator fun Num.plus(rightValue: Num) = Num(n + rightValue.n)
Num(3) + Num(4)
```
While using Kotlin, overloaded operators are everywhere. For example, accessing a list with `[]`, `+=`. etc. is all done by default overloaded operators.
In data classes, the `componentN` functions can be overloaded to retrieve the member items through destructuring operators.
```kotlin
data class Person(val name: String, val age: Int) {
	operator fun component1(): String {
		return name
	}
	operator fun component2(): String {
		return age
	}
}
val(name, age) = val Person("John", 54)
```

## Lazy initialization
Kotlin offers the `lazy()` function to delay the initialization of a value to only happen when it is first used. This can be handy in situations where initialization is expensive or if the variable might not be used.
```kotlin
val late by lazy { expensiveCalculation() }
if (needsMath) {
	// Only when it is needed will the value be available
	return late
}
```

## Late initialization
Kotlin offers the `lateinit` keyword to delay initialization to a later time decided by another component. This is often used through libraries. For example, if a library ensures that a specific variable will be initialized.
```kotlin
// Kotlin program to demonstrate how to check
// whether lateinit variable is initialized or not
class GFG {
	
	// Declaring a lateinit variable of Int type
	lateinit var myVariable: String
	fun initializeName() {
		
		// Check using isInitialized method
		println("Is myVariable initialized? " + this::myVariable.isInitialized)
		
		// initializing myVariable
		myVariable = "GFG"
		
		// Check using isInitialized method
		println("Is myVariable initialized? " + this::myVariable.isInitialized)
	}
}

fun main(args: Array<String>) {
	
	// Calling method
	GFG().initializeName()
}
```
