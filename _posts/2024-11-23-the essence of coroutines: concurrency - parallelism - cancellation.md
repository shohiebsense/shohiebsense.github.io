[https://youtu.be/kIzjzjJGk0Y](https://youtu.be/kIzjzjJGk0Y)

![img](https://github.com/shohiebsense/shohiebsense.github.io/blob/master/images/Screenshot%202024-11-23%20at%2013.15.00.png?raw=true)

`yield()` in this context is similar way to do a pause.  

Likewise the counterpart of it is `resume()`

so the goal is how to make a function return, can do some 'pause' while preserving its state, and can be a value.  

```kotlin
fun main() {
    var cow = 0
    println("Milking cow #${++cow}")
    feedChickens.resume()
    println("Milking cow #${++cow}")
    feedChickens.resume()
    println("Milking cow #${++cow}")
    feedChickens.resume()
    println("Milking cow #${++cow}")
    feedChickens.resume()
}

val feedChickens = createCoroutine {
    var chicken = 0
    println("Feeding chicken #${++chicken}")
    yield()
    println("Feeding chicken #${++chicken}")
    yield()
    println("Feeding chicken #${++chicken}")
    yield()
    println("Feeding chicken #${++chicken}")
    complete()
}
```

 uses a coroutine (createCoroutine) to interleave tasks between milking cows and feeding chickens.  
 The yield() function allows the coroutine to pause, returning control to the main function.  

 The yield() keyword in Kotlin coroutines suspends the execution of the current coroutine,  
 allowing other coroutines or the calling function to continue executing.  
 It effectively "pauses" the coroutine at that point, allowing the main function to regain control and perform other tasks,  
 such as incrementing and printing the cow counter in the example.

This allows for cooperative multitasking,  
where the coroutine voluntarily yields execution without blocking the entire thread,  
facilitating efficient interleaving of operations.
