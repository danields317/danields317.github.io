# Functional
This document contains a summary of functional programming features available in Kotlin.

## Lambdas
Lambdas are anonymous functions with a shorter syntax. The last statement of a lambda function is also what it will return.
When a lambda is used as the only or last argument in a function (e.g. in `map()`) the `()` can be omitted and the lambda can be placed directly after the function name. When a function takes a lambda as argument, the lambda needs to follow the pattern of amount of arguments and return type specified by the function.
```kotlin
{ one: Int, two: Int -> one + two }
{ println("HI") } // Lambdas without arguments don't need the arrow
values.map { it + 1 }

// Lambdas can be stored in variables
val resusable = {e: Int -> e + e}
values.map(reusable)
```

Kotlin lambdas are statically scoped and can interact with the environment they are created in. The example below shows that a lambda function is made in class One and a reference to the lambda is given to class Two. Even when executing it through class Two it can update number in class One.
```kotlin
class One {
    var number = 5
    val adder = { number += 1 }
}

// Require a value called 'f' of type Lambda without arguments returning a unit
class Two(val f: () -> Unit) {
    fun execute() {
	    f()
    }
}

fun main() {
    val one = One()
    println(one.number)
    one.adder()
    println(one.number)
    val two = Two(one.adder)
    two.f()
    println(one.number)
}
```

## Operations on Collections
Kotlin offers a bunch of functions on collection objects (e.g. lists, maps, etc.) to perform operations on its contents. These functions take lambdas as a parameter that will be run for each item in the collection. Examples of these are `filter()`, `find` or `map()`. 
It is of course possible to write a `for` loop and add the lambda logic in the body, but it is recommended to use the offered functions when possible. This is because it will reduce in less code and less chances of bugs.

## Member References
Kotlin offers the `::` operator to create a reference to a variable, function or constructor.
These references can be used in a few special ways.

Using this on variables returns an object of type `KProperty<datatype>`. The original variable can be edited through this reference object.
The reference object can be used as a function and it will return the value in the field. This reference as a function can be passed to functions that require a function that expects 1 generic argument and returns 1 value of that data type. 
For example, the `filter` method takes an argument of the type of data in the collection (so it is generic by default) and it should return a Boolean to determine if the item should be filtered out or not. It is possible to give a reference to a Boolean value here.

```kotlin
data class Thing(val isReal: Boolean) 

fun main() {
	var things = listOf(Thing(true), Thing(false))
	things = things.filter(Thing::isReal)
    println(things.size)
}
```


Using this on functions returns an object of `KFunction<List of Argument, Return Type>`
Function references can be used to pass a regular function as a lambda to functions that ask for one. As long as the arguments and return type match the requirements of the lambda similar to `KProperty`. This also works for extension functions.
```kotlin
class Thing() {
	fun isTrue(val item: Bool) = item
}

val thing = Thing
list.filter(Thing::isTrue)
```

Using this on constructors returns an object of `KFunction<Arguments, Object Type>`.
It can be used in situation where a program expects a function object that takes the same parameters as the constructor and returns an object of said class.
```kotlin
class Thing(val text: String) {

}
list.map(::Thing)
```

## Zipping and Flattening lists
Two handy to know list functions are `zip` and `flatten`.
The `zip` function is used to combine two lists. Element at the same position in the two lists are zipped after each other. So when given `list1` and `list2` the resulting list will look like `[list1[0], list2[0], list1[1], list2[1]]` etc.

The `flatten` function takes a list of lists extracts the values in the inner lists into one list.

## Sequences
Sequences are the Kotlin implementation of what is usually called Streams in other languages. Sequences are a collection of data that can be iterated over but cannot be indexed (so no `list[2]` for example). Sequences work through Lazy Evaluation (instead of eager). This means that code is only executed when a result is required. Streams work with intermediate and terminal functions. Intermediate functions return another stream and terminal functions return a result. So only when a terminal function is executed, a stream will start working.

```kotlin
val result = (1..10).asSequence()
	.filter { it % 2 == 0 } // 1 gets filtered out, continues to 2
    .map { it * 2 } // 2 * 2 = 4
    .first() // Returns 4 and stops since first() is satisfied with 1 item
```

> [!NOTE]
> Eager Evaluation, which is used in lists, maps, etc. is also named Horizontal Evaluation. This is because each operation is performed on the entire list before going to the next operation in the chain. 
> Lazy Evaluation is also called Vertical Evaluation. This is because each value in the collection goes through the chain of operators first all the way until the terminal statement. If the terminal statement is satisfied with the currently processed items, the rest of the items don't have to be processed anymore.

## Local Functions
Functions can also be specified inside of other functions. It is also possible to create anonymous functions.

```kotlin
fun doThis() {
	fun doMore() {
		println("Hi")
	}
	while(true) { doMore() }
	while(true) {
		fun() {
			println("HI")
		}
	}
}
```

## Labels
When returning from a lambda, it will also return from the function. To only return out of the function it was called from, a label can be used.
```kotlin
fun main() {
    val numbers = listOf(1, 2, 3, 4, 5)
    numbers.forEach label@{ // "label@" defines a label for the lambda
        if (it == 3) {
            println("Skipping $it")
            return@label // Return from the lambda, not the entire function
        }
        println("Processing $it")
    }
    println("Finished processing!")
}
```

## Folding
Folding is a technique to combine all items of a list into one value. A fold function takes a function with two arguments: the accumulator and an item. The accumulator contains the first item of a list initially and the item contains the next one. The function in the fold can then do any operation in which the item gets added to the accumulator. Then this accumulated item gets passed to the next iteration of the fold together with the next item in the list.

```kotlin
fun main() {
    val words = listOf("Kotlin", "is", "awesome")
    val sentence = words.fold("Sentence:") { accumulator, word ->
        "$accumulator $word"
    }
    println(sentence)
}
```

## Recursion
Recursion is a technique where a function calls itself. Recursion can result in `StackoverflowError` if the recursion goes to deep. This can be prevented by writing a recursive function with tail recursion. In Kotlin, the `tailrec` keyword needs to be specified to create a tail recursive function. If a `tailrec` function is not actually a functioning tail recursive function, Kotlin will produce an error.

```kotlin
tailrec fun factorialTailRec(n: Int, accumulator: Int = 1): Int {
    if (n <= 1) {
        return accumulator
    }
    return factorialTailRec(n - 1, n * accumulator)
}
```