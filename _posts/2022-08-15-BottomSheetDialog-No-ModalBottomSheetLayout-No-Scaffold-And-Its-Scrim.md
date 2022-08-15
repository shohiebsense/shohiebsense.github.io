Say you want to make a BottomSheetDialog that:
1. Has no Scrim Layout  
2. Can do interaction behind it (its main layout)
3. Just a simple one (visible and inVisible), 
4. As for implications there's no need `modalBottomSheetState` just visible (expand) and hide (invisible)

Have a look at the codebase [here](https://cs.android.com/androidx/platform/frameworks/support/+/androidx-main:compose/material/material/src/commonMain/kotlin/androidx/compose/material/ModalBottomSheet.kt), the `ModalBottomSheetLayout()` part  

You realize the `ModalBottomSheetLayout` is using `BoxConstraintLayout`  

Skip the `Box()` and its `Scrim()` one, they are the `MainContent()`

Just hop in to the `Surface` that is the `ModalBottomSheetContent()` from API  

You can get them as a reference  

The key is the `offset{}` `Modifier`  

Then you can use `BoxConstraints(){constraints.maxHeight}` to get the layout fullHeight,  

The default alignment is `Top`, assuming `maxHeight` takes a whole screen, then use the offset with `y` using that value  

If you want to get the content height, use the `onGloballyPositioned{}` remember the height there  


```kotlin
 val sheetHeightState = remember { mutableStateOf(0) }

 ..
 Modifier
 .onGloballyPositioned {
    sheetHeightState.value = it.size.height
 }
```
Now you get the height of that layout, substract the `maxHeight` with it.  
Make use of the `animateIntOffsetAsState()` to apply `Modifier.offset{}`

```kotlin
val currentHeight = animateIntOffsetAsState(targetValue = IntOffset(0, if(isVisible) maxHeight -  sheetHeightState.value  else maxHeight))
```

apply it to the `Surface`

```kotlin
@ExperimentalFoundationApi
@ExperimentalMaterialApi
@Composable
private fun CustomDialog(
    isVisible: Boolean,
    modifier : Modifier = Modifier,
) {

    BoxWithConstraints(modifier) {
        val fullHeight = constraints.maxHeight
        val sheetHeightState = remember { mutableStateOf(0) }

        val currentHeight = animateIntOffsetAsState(targetValue = IntOffset(0, if(isVisible) fullHeight -  sheetHeightState.value  else fullHeight))

        Surface(
            Modifier
                .fillMaxWidth()
                .offset {
                    currentHeight.value
                }
                .onGloballyPositioned {
                    sheetHeightState.value = it.size.height
                },
            shape = BottomDialogShape,
            elevation = 0.dp,
            color = Color.Transparent,
            contentColor = Color.Transparent
        ) {
            Column {
                ModalBottomSheetContent()
            }
        }
    }
}
```
