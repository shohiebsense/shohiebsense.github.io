1. Make a class that implements `RippleTheme`

Sample: 
 ```kotlin
 
 class CustomRippleTheme(private val rippleColor: Color) : RippleTheme {

    //Your custom implementation...
    @Composable
    override fun defaultColor() =
        RippleTheme.defaultRippleColor(
            rippleColor,
            lightTheme = MaterialTheme.colors.isLight
        )

    @Composable
    override fun rippleAlpha(): RippleAlpha =
        RippleTheme.defaultRippleAlpha(
            rippleColor.copy(alpha = 0.75f),
            lightTheme = MaterialTheme.colors.isLight
        )
}

 ```

2. Wrap your component that you want to be clicked with `CompositionLocalProvider`, asssociate a CompositionLocal key to `YourCustomRippleTheme` as a value in the `values` argument

```kotlin
CompositionLocalProvider(LocalRippleTheme provides CustomRippleTheme(color: DesiredColor){
  //your composable (component)
}

```

3. If it is not a `Button` you can add `clickable{}` Modifier, no need to add other arguments

```kotlin
modifier = Modifier.clickable{}
```
