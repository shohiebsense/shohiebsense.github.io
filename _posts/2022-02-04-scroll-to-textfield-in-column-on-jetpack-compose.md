1. You can either use ``BringIntoViewRequester`` read about it [here](https://medium.com/tech-takeaways/automatic-scrolling-to-composable-on-focus-change-with-bringintoviewrequester-in-jetpack-compose-bdeb72242bac)
Read the documentation [here](https://developer.android.com/reference/kotlin/androidx/compose/foundation/relocation/BringIntoViewRequester)

2. Or, use ``Modifier.onGloballyPositioned { coordinates -> //save the value }``

create an object that stores your textfield state (position) say `textFieldState`.


```kotlin
  fun onGloballyPositioned(coordinates: LayoutCoordinates) {
        scrollPosition = coordinates.positionInWindow().y.toInt()   
  }
```

next, getKeyboardVisibility

```kotlin
@Composable
fun getKeyboardVisibility(): State<Boolean> {
    val keyboardState = remember { mutableStateOf(false) }
    val view = LocalView.current
    DisposableEffect(view) {
        val onGlobalListener = ViewTreeObserver.OnGlobalLayoutListener {
            val rect = Rect()
            view.getWindowVisibleDisplayFrame(rect)
            val screenHeight = view.rootView.height
            val keypadHeight = screenHeight - rect.bottom
            keyboardState.value = keypadHeight > screenHeight * 0.15
        }
        view.viewTreeObserver.addOnGlobalLayoutListener(onGlobalListener)

        onDispose {
            view.viewTreeObserver.removeOnGlobalLayoutListener(onGlobalListener)
        }
    }
    return keyboardState
}
```

then, handle it, every textfield on your screen.

```kotlin
@ExperimentalComposeUiApi
@Composable
fun HandleBottomTextField(
    isKeyboardVisible: Boolean,
    scrollState: ScrollState,
    vararg textFieldStateList: BaseTextFieldState,
    bottomInset: Int,
    isTheLastScrollToBottom: Boolean = true,
    coroutineScope: CoroutineScope,
) {
    textFieldStateList.forEachIndexed { _, textFieldState ->
        if (textFieldState.isFocused.value && isKeyboardVisible) {
            LaunchedEffect(
                textFieldState.isFocused.value,
                isKeyboardVisible
            ) {
                coroutineScope.launch {
                    delay(CommonUtil.DEFAULT_DELAY_SCROLL_IN_MILLISECONDS)
                    if(textFieldState == textFieldStateList.last() ||
                        textFieldState == textFieldStateList[textFieldStateList.lastIndex-1]){
                        scrollState.animateScrollTo(scrollState.maxValue)
                    } else {
                        scrollState.animateScrollBy(getScrollByValue(textFieldState.scrollPosition > 450, textFieldState.scrollPosition))
                    }
                }
            }
        }
    }
}
```
you can adjust yourself regarding the value
```kotlin
fun getScrollByValue(isPositionBelowCurrentScrollState: Boolean,
                     textFieldScrollPosition: Int) : Float {
    if(isPositionBelowCurrentScrollState){
        val scrollByValue = textFieldScrollPosition - 450
        return scrollByValue.toFloat()
    } else {
        val scrollByValue = 450 - textFieldScrollPosition
        return -scrollByValue.toFloat()
    }
}
```

there it goes
![Action](https://i.postimg.cc/7ZvrhHNt/Record-2022-02-04-16-07-43-753.gif)
