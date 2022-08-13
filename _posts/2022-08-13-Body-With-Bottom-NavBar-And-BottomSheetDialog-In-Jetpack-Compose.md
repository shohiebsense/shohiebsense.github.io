You can mix the `ModalBottomSheetLayout` and `Scaffold`, put the `Scaffold` inside `ModalBottomSheetLayout` `@Composable content()`  

Sample  

```kotlin
ModalBottomSheetLayout(
    sheetState = modalBottomSheetState,
    sheetElevation = 0.dp,
    sheetBackgroundColor = Color.Transparent,
    sheetContentColor = Color.Transparent,
    sheetShape = BottomDialogShape,
    sheetContent = {
        yourcustomSheetContent()
        CommonBottomSheetStyledDialog(
            componentParameter = componentParameter,
            dialogType = dialogType,
            dialogStringResIdPair = dialogTitleDescResIdPair,
            onDismiss = onDialogDismiss
        )
    },
    modifier =
        Modifier.then(statusBarModifier)
            .navigationBarsPadding() // info no need ro add with imepadding if doesnt required
            // keyboard
            .fillMaxSize()
) {
    Scaffold(
        backgroundColor = backgroundColor,
        scaffoldState = scaffoldState,
        topBar = topBar,
        bottomBar = {
            YourBottomNavBar(
                activePosition = bottomNavPosition,
                componentParameter = componentParameter,
                navController = navController
            )
        },
        floatingActionButton = {
            YourFloatingActionButton(componentParameter = componentParameter) {
                // todo
            }
        },
        floatingActionButtonPosition = FabPosition.Center,
        isFloatingActionButtonDocked = true,
    ) {
        content(it)
    }

    //OtherComposable()
}

```
