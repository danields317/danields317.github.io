# Basics
This document contains a summary of the basic aspects of coroutines in Kotlin.

## The coroutine
A coroutine is an instance of a suspendable computation. It is conceptually similar to a thread, in the sense that it takes a block of code to run that works concurrently with the rest of the code. However, a coroutine is not bound to any particular thread. It may suspend its execution in one thread and resume in another one. Because multiple coroutines be run on the same thread, they are very light weight. No heavy, memory intensive operations have to be done to start them.

To start a coroutine, a scope for the coroutine needs to be defined first. This scope will indicate the how the coroutines will behave alongside the non-concurrent environment. The most basic one is `runBlocking`. This scope indicates that all coroutines must finish before continuing in the sequential world.
Then inside of a scope, the `launch` method is available. The code defined as the argument to launch will be run as a coroutine.

```kotlin
fun main() { runBlocking { 
    launch {
	    // Simulate delay
        delay(1000L) 
        println("World!")
    }
    // Executes the moment the coroutine started
    println("Hello")
}
// Due to runBlocking only executes after finishing the scope.
println("Done!") 
}
```

## Suspend functions
Certain functions like `delay` are only available in the context of a coroutine. When writing code to execute directly in `launch`, it will be clear to the compiler that this code runs in the context of a coroutine so all features are available. But when code gets larger, features should be extracted to functions and the compiler cannot tell if a function will be run in the context of a coroutine. To tell Kotlin that a function is designed for coroutine usage, the `suspend` keyword is used.

```kotlin
fun main() = runBlocking { // this: CoroutineScope
    launch { doWorld() }
    println("Hello")
}

// this is your first suspending function
suspend fun doWorld() {
    delay(1000L)
    println("World!")
}
```

## Scope builder
The top level scopes like `runBlocking`, block the entire thread underneath while waiting for the coroutines inside it to finish. It is possible to create additional scopes inside of a top level scope through the `coroutineScope` function. This performs similar to `runBlocking`, waiting for the coroutines inside to finish before continuing. But instead of blocking the entire thread, it only blocks that scope. With these nested scopes, multiple blocks can be created inside of one top level block. Giving more control over execution without having to create multiple top levels.

```kotlin
// Start a top level scope
fun main() = runBlocking {
	// Start a sub level scope.
    doWorld(1)
    // Only starts running when the previous sub level scope finished
    doWorld(2)
    println("Done")
}

suspend fun doWorld(number: Int) = coroutineScope {
    launch {
        delay(2000L)
        println("Country $number")
    }
    launch {
        delay(1000L)
        println("World $number")
    }
    println("Hello")
}
```

## Jobs
The `launch` function returns a `Job` object that represents the coroutine. This object can be used to manage the coroutine.
```kotlin
val job: Job = launch {
    delay(1000L)
    println("World!")
}
println("Hello")
job.join() // wait until child coroutine completes
println("Done") 
```