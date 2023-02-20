1. Either you can use Interface and delegate (implement) it to viewModel (act as a Contract) or  
2. Make a class but initialize inside viewModel, `val` is much preferred 

viewModel itself has already been `remembered`, so the class no need to be `remembered` either  

Either I have to accept the fact that initialize `mutableState` is ugly inside a class or just get over it with those number of arguments.  

OR

Using `ProvidableCompositionLocal<T>`  

Read about it [here](https://developer.android.com/reference/kotlin/androidx/compose/runtime/CompositionLocal)  

for example  

```kotlin
fun LocalComponentParameter(isDarkTheme: Boolean, screenDimensionIndex: Int) =
    compositionLocalOf {
        ComponentParameter(
            backgroundColorIndex = isDarkTheme.toInt(),
            screenDimensionIndex = screenDimensionIndex
        )
    }
    
val componentParameter: ComponentParameter
    @Composable
    @ReadOnlyComposable
    get() = LocalComponentParameter(
        isSystemInDarkTheme(),
        integerResource(id = R.integer.screen_dimension)
    ).current
    
```

since we need it in composable functions, by design, it is to answer the problem.  

