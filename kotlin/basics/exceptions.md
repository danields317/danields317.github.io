# Exception Handling
This document contains a summary of Exception Handling features in Kotlin.

## Exception throwing
Exceptions can be thrown with the `throw` keyword. All classes that derive from `Throwable` can be thrown. The default exception class implements `Throwable` and custom exceptions can be created by implementing the `Exception` class.
```kotlin
class NewException(
	description: String
): Exception(descriptioin)

throw NewException("This went wrong")
```

## Recovery
Exceptions are handled through a `try catch` block. Multiple `catch` blocks, all catching different exceptions can be put underneath a `try` block. Exceptions will be caught if the class they are derived from is one of the `catch` blocks. E.g. all exceptions are caught when `exception` is one of the blocks.
```kotlin
try {
	runSomething()
} catch (e: NewException) {
	println("The new one!")
} catch (e: Exception) {
	println("Something else went wrong")
}
```

## Resource Cleanup
Kotlin uses the `finally` keyword to handle any type of action that needs to be done no matter if try succeeds or fails. 
```kotlin
try {
 something()
} catch(e: Exception) {
	println("handling")
} finally {
	println("always runs")
}
```

## Check Instructions
Checking if the data an application uses is compliant with the business logic is commonly done. For example, when processing numbers that represent dates, numbers representing months should be between 1 and 12. Kotlin offers the `require()` method to handle this easily. This will return an `IllegalArgumentException` if the condition is not met.
```kotlin
fun printMonth(month: Int) {
	require(month in 1..12) {
		"Not a month number"
	}
}
```

`requireNotNull()` is a special version of `require` that throws an error when the given argument is null. If it is not, the input value is smart casted to be not nullable in the statements after the check.

```kotlin
fun printMonth(month: Int?) {
	requireNotNull(month) {
		"Not a month number"
	}
	// It is now smart casted to Int from Int? due to the check
	month + month
}
```

`check()` is a function similar to `require()` but will throw an `IllegalStateException` if the statement resolves to false. This function should be used at the end of a function to verify if it created the result that was expected. This is usually only used in unit tests but if needed can be used in regular code.

`assert()` is also similar to `require()` and `check()` but is not turned on by default. Using the command line flag `-ea` will turn on the `assert` statements. The benefit of this is that these statements can be added all over the codebase and will only be run when explicitly asked for. So the assertions can be run during testing and can be turned off when deploying without having to touch the code. But usually these are also only used in unit tests.

## Nothing type
In certain cases it is possible that a function does not return anything at all (not even `unit`). For these cases, the `Nothing` type exists. For example, functions that always throw an error or are an infinite loop will not return anything.
```kotlin
fun doError(): Nothing {
	throw Exception()
}
```

## Errors in resource cleanup
When trying to clean up complex resources in a `finally` block, it might be possible that the cleanup produces more errors. Kotlin can help with this through its `use()` functions that can be used on any object that implements the `AutoClosable` interface. Kotlin will figure out the cleanup of the resource behind the scenes to not interfere with the other errors. The `DataFile` class, which allows reading and writing files implements this interface.

## Logging
Logging in Kotlin is usually done with the following open source package [Kotlin-Logging](https://github.com/oshai/kotlin-logging). This package (and most other logging tools), have the following log levels.
- `trace()` for step by step detailed information about the operations in the application.
- `debug()` for detailed information that can be helpful while debugging (e.g. inputs and outputs) the application.
- `info()` for general information about normal operations and key events in the application.
- `warn()` for potential issues and unexpected situations that do not cause immediate problems to the application.
- `error()` for issues or failures that prevent desired execution of the application.
An application can be run on different log levels, depending on the specified level a subset of the logs will be printed.

---
[Power Tools](tools.md)