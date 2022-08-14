yeah, for the requirement, it should be in different sub-classes

```markdown
Calling Function in a class  -->  the entity in a calling function class  -> **the entity that is placed to emit source of truth**
|
|
------------------------>         the other entity in a calling function class -> **the entity that collects the source **
 ```
 
 If it's in the same structure of calling class, then, there's no need, the ability will be wasted anyway. Just handle it in the calling function class.  
 If it's similar to that case up there, then proceed to make a cleaner, lazier way like as follows
 
 1. Make an Interface that contains a desired MutableSharedFlow<YourDesiredEntityToEmit>  
 2. Implements both the entity that has source to emit and the entity that collects it with that Interface  
 3. using `yourMutableSharedFlow.emit(YourDesiredEntityToEmit)` wrap it inside a `coroutineScope` inside a class that will emit the source    
  
  sample    
  ```kotlin
fun onSourceOfTruthCaptured(sourceOfTruth: T) {
    coroutineScope.launch { yourMutableSharedFlow.emit(sourceOfTruth) }
}
  ```
 4. using `yourMutableSharedFlow.collect{ yourEntity -> }` call it in the class that will collect the emitted source, after you initialize the class, and wrap it inside a `coroutineScope`  
  
  sample    
  ```kotlin
  fun init(){
    coroutineScope.launch {
        yourMutableSharedFlow.collect { it ->
            handleIt(it)
        }
    }
}
```  
