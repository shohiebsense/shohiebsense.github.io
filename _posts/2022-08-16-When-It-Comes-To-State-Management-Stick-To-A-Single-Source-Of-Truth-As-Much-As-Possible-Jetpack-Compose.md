Right,  

1. When it's `arrayList`, have some confidence that the key in the `LaunchedEffect`, `arrayList` itself should be enough
2. When it comes to nested array, or anything complex that requires a reference/associate, have a look at tuples (pair), `associateBy()` or `associate()`, 
    mix it with `MutableStateList` works well.  
3. Avoid using `SideEffects` in the loop if it's possible, it greatly affects the performance, still if you have to, don't make a higher time complexity code
4. Also, `set()` function of an `arrayList` or just directly use` yourList[index]` works well triggering `SideEffects` of Jetpack Compose, no need to `remove` then `add`
5. Like you read that title, once again I'm saying, stick it to one reference, if you placed in a `viewModel`, just refer to it only.
    it won't work if you try to manipulate a list that makes it has a new reference to a variable again with desired criteria (filtered, sublisted, etc.), but for helpers (just for read-only variable, OK)
6. Wrap Using `SideEffects` if it's a direct parent of an element, say,  you want to make a trigger after doing action on an element of the array, then wrap it using that direct array
  
Example

```kotlin
    val isMonthlyDataCheckedList = mutableStateListOf<Pair<Boolean, SnapshotStateList<Pair<Boolean, Boolean>>>>()
    
```  

The `LaunchedEffect` will be  
```kotlin
if ( viewModel.isMonthlyDataCheckedList.any { monthlyData -> monthlyData.second.any { it.second } }) {
    LaunchedEffect(
        viewModel.isMonthlyDataCheckedList.any { dailyData -> dailyData.second.any { it.second } }
    ) {
        //yourCode
    }
}

```
