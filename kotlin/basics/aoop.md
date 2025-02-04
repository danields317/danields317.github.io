# Kotlin Advanced Object Oriented Programming
This document contains a summary of advanced Object Oriented Programming features and concepts in Kotlin.

## Interfaces
An interface is defined with `interface` keyword. Any class implementing an interface has to mark each overridden function or variable with `override`.
Interfaces can also be used in `enum` classes. Then each `enum` value can define their own implementation for the interface value. 

```kotlin
interface Sound {
	fun makeSound(): String
}

class Microphone : Sound {
	override fun makeSound(): String {
		return "Singing!"
	}
}
```

### SAM Conversions
Single Abstract Method is an approach to interfaces where the interface only has one method. In Kotlin this can be explicitly defined through `fun interface`. Kotlin will then enforce this rule of only having one function.
It is also possible to instantiate SAM interfaces by passing a lambda to the interface. This will return an object with the method implement through the lambda.

```kotlin
fun interface Adder {
	fun add(one: Int, two: Int): Int
}

class Calculator: Adder {
	override fun add(one: Int, two: Int) {
		return one + two
	}
}
val lambda = Adder {one, two -> one + two}
lambda.add(1, 2)
```

## Complex Constructors
For additional code to run during object construction, Kotlin uses `init` blocks.
```kotlin
class Message(text: String) {
	// A property can still be val when initialized through init!
	private val content: String
	init {
		content = "Hi $text"
	}
}
```

## Secondary Constructors
When a class requires multiple different constructors, Kotlin offers the `constructor` block. The first statement in a secondary constructor must be to call another constructor until the main constructor has been called. This is needed because properties can be initialized directly in the main constructor and additional logic might depend on this. The other constructors are called with the `: this()` syntax behind the `constructor` method name.

```kotlin
class WithSecondary(i: Int) { 
	init { 
		trace("Primary: $i") 
	} 
	
	constructor(c: Int, d, Int) : this(c + d) { 
		trace("Secondary: '$c'") 
	}
```

## Inheritance
To inherit from a regular class, Kotlin uses similar syntax to interfaces but requires `()` to be added after the class. For a class and its members to be used for inheritance they also have to be marked as `open`.  To call the base class methods, the `super` keyword can be used.

```kotlin
open class Ape {
	open fun eatBanana() {println("Yummy")}
	open fun makeSound() {println("OOH AAH AAH")}
}

class Human: Ape() {
	override fun makeSound() {println("I hate doing taxes")}
	override fun eatBanana() {
		println("Let me peel the banana first")
		super.eatBanana()
	}
}
```

## Base Class Initialisation
When a base class expects values in its constructor, the derived class must deliver these values. Kotlin calls the constructor of the base class first and then goes down the inheritance chain. This way, values from the base class are available during initialisation of the derived classes.
```kotlin
open class SuperClass1(val i: Int) 
class SubClass1(i: Int) : SuperClass1(i)
```

## Abstract classes
Kotlin uses the `abstract` modifier to define abstract classes, variables and functions.
```kotlin
abstract class doHalf() {
	abstract val pleaseImplement: String
	val message: String = "HI"
	abstract fun doFirst()
	fun doSecond() { println("HI")}
}
```
Abstract classes differ from interfaces through their feature to hold state. Any properties defined in an interface are only stored in the class implementing it. Properties in abstract classes can actually be stored in the abstract class. When a property is defined as `abstract`, it needs to be overridden. But regular properties can be used directly.

## Upcasting
Upcasting is the process of using a derived class like it is the base class. Through this feature, one piece of code that can use the base class can be written instead of having to develop an implementation for each derived class.
```kotlin
interface Derivable {
	fun doThis()
}
fun execute(der: Derivable) {
	der.doThis()
}
```
Upcasting is a feature used in inheritance situations. If an inheritance structure is set up, upcasting needs to be used to make use of it. Without upcasting, all derived classes would be used directly and any base classes are practically unused.

There are two programming principles around upcasting that are important.

*Prefer composition to inheritance*. Inheritance creates a tight coupling between the base class and the derived class. Composition is a technique where a class gets its functionality and data through storing it directly in the class. This is a less tight coupling.
```kotlin
class NoiseMaker(val sound: String) {
	fun makeNoise() {
		println(sound)
	}
}
class Dog(val noiseMaker: NoiseMaker) {
	fun bark() {
		noiseMaker.makeNoise()
	}
}
val dog = Dog(NoiseMaker("Bark"))
```

*Liskov Substitution Principle*. This principle means that in any place a base class is used, the derived class should be usable as well. This means that a derived class should not break any of the functionality of the base class.

## Polymorphism
Polymorphism is the concept of using an object as its upcasted version. When a derived class is passed to a statement that expects the base class, only the base class members are usable. But when calling these members, their implementation of the derived class is used.

## Composition
Composition is the technique of putting a class inside of another to class to chance the functionality. This way, the class that receives another class can have different behaviours depending on the instance of the given class. An example of this is shown in the code block above.

## Class Delegation
When using inheritance, functions defined in the base class are also exposed and usable through the derived class. When using composition, this is not the case. Kotlin offers a way to bridge the gap between the accessibility of inheritance and the practical usage of composition with the keyword `by`.

```kotlin
// Create an interface to define the functions
interface Clicker {
	open fun click(): String
}

// Make an implementation for the interface
class Mouse(): Clicker {
	override fun click() {
		return "Click with mouse!"
	}
}

// Through composition add to another class
class Computer(
	private val mouse: Clicker: Mouse()
): Clicker by mouse // Expose given interface through member

// Now the interface is directly accessible
// Otherwise requires computer.mouse.click()
val computer = Computer()
computer.click()
```

## Downcasting
Downcasting is the process of identifying a derived class when it is referenced as the base class. Kotlin offers a few ways to do this.
The `is` keyword checks if a class is of a certain type. When used in an `if` or `when` block, Kotlin automatically casts the object to the derived class inside of the block for easy usage.
```kotlin
val b1: Base = Derived1() // Upcast 
if(b1 is Derived1) 
	b1.g() // Within scope of "is" check 
val b2: Base = Derived2() // Upcast 
if(b2 is Derived2) 
	b2.h() // Within scope of "is" check
	
when (c) { 
	is Human -> c.greeting() 
	is Dog -> c.bark() 
	is Alien -> c.mobility() else -> "Something else" 
}
```

These smart casts only work when the object is stored as a `val`. This is because a `var` could be set to another object right after the check but before the execution. A workaround of this is copying the `var` to a `val` to do the check. E.g. `when(val c = c)` copies a `var` to a `val` local to the `when` block.

It is possible to force an object to cast to a specific datatype with `as`. This is unsafe since it is possible that the datatype cannot be cast and will throw an exception. It is also possible to use `as?` which returns null when the cast cannot be done instead of an exception.
```kotlin
fun dogBarkSafe(c: Creature) = (c as? Dog)?.bark() ?: "Not a Dog"
```

## Sealed classes
The `sealed` class modifier can be used to force derived classes to be defined in the same file as the base class. This is an alternative to the `open` modifier which allows derived classes to be specified anywhere. Because no derived classes can be made outside of the file, the compiler will know all the possible derived classes during compilation. E.g. when the created app is used as a library, the library user cannot add additional derived classes as with an `open` class.
The biggest benefit of this is that a `when` statement does not need an `else` branch anymore as long as a branch has been made for each derived class.
Sealed classes work like abstract classes besides the 'sealing' feature.
```kotlin
sealed class Top 
class Middle1 : Top() 
class Middle2 : Top()
// Marking a derived class open allows extending from anywhere again
open class Middle3 : Top() 
class Bottom3 : Middle3()
```

The `::class` statement generates a class object. This object holds properties with information about the class. One of these is `sealedSubclasses`, which holds information about all derived classes of a sealed class.
```kotlin
fun main() { 
	Top::class.sealedSubclasses.map { it.simpleName } 
	// "[Middle1, Middle2, Middle3]" }
```

## Nested classes
A class can be nested inside of another class, a function or an interface. This can help improve the logical structure of a system. Enums can also be nested inside of a class.

Classes nested inside of a function are only accessible from within that function. This should rarely be used. Nesting a class in any of the other scopes might improve readability and the logical structure but serves no technical benefits.

## Objects
Kotlin offers the `object` keyword to create so called Singleton's. An object is defined similar to a class but there will always just be one instance. The object is available through its name. Objects can inherit from interfaces, abstract classes and open classes.
```kotlin
object Counter {
	var count = 0
	fun plus() {
		count++
	}
	fun minus() {
		count--
	}
}

Counter.plus()
Counter.minus()
```

## Inner classes
The inner classes feature allows the creation of a nested class that is referenced to its parent class. To create an inner class, an instance of the outer class has to be made first. The instance of the outer class can then reference the data in the instance of the outer class instance.
When using inner classes, use the `this@<classname>` to specify which class to reference in cases where this is ambiguous. 
```kotlin
class House(val number: String) {
	inner class Room(val number: String) {
		fun show() {
			// Use house number not room number
			println(this@House.number)
		}
	}
}
val house = House("15")
val room = house.Room("1")
room.show() // 15
```
It is possible to use an inner class as a base class in inheritance situations.
Inner classes can also be used as local and anonymous classes.

## Companion objects
A companion object is an object that is linked to a class instead of being a separate singleton. The companion object is accessible through instances of the related class but there is still only one instance of the companion. So data from the companion is shared between instances.
```kotlin
class House() {
	companion object {
		var counter = 0
		fun plus() {
			counter++
		}
	}
}
val house = House()
house.plus()
```

---
[Next Chapter](exceptions.md)