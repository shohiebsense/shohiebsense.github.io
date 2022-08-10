Simply, meet the conditions from one to another for chaining animation.  

For example: Scale -> Expand -> Alpha Animation 

assuming scale is float, let it `animateTo` with your `desiredValue`  

next, execute the `expand` within a `Side-Effect`, `LaunchedEffect` is enough  

next method is similar, using `LaunchedEffect` execute your alphaAnimation using `animateTo` to your `desiredValue`  

sample:

```kotlin
    
@Composable
YourAnimatedComposable() {
    val shapeRadius: Float
    with(LocalDensity.current) { shapeRadius = 10.dp.toPx() }
    var radius by remember { mutableStateOf(particleRadius) }
    var visibilityAlpha by remember { mutableStateOf(0f) }
    var visibilityAlphaTitleRow by remember { mutableStateOf(0f) }
    val isVisible = remember { mutableStateOf(false) }

    val animatedRadius = remember { Animatable(shapeRadius) }
    val animatedRadiusTitle = remember { Animatable(shapeRadius) }
    val animatedAlpha = remember { Animatable(0f) }
    val animatedAlphaTitle = remember { Animatable(0f) }

    val visible by derivedStateOf { radius }
    val isContentVisible by derivedStateOf { radius >= maxRadiusPx * 0.8f }

    YourComposable(
        modifier =
            Modifier.onGloballyPositioned { coordinates ->
                    if (maxRadiusPx == 0f) {
                        maxRadiusPx =
                            hypot(coordinates.size.width / 2f, coordinates.size.height / 2f)
                    }
                }
                .drawBehind {
                    drawCircle(
                        color =
                            if (isVisible.value)
                                Edufund_Background_Color_List[
                                    componentParameter.backgroundColorIndex]
                            else
                                Edufund_Background2_Color_List[
                                    componentParameter.backgroundColorIndex],
                        radius = radius
                    )
                }
                .alpha(visibilityAlphaTitleRow)
    ) {
        // otherComposables
    }
    AnimatedVisibility(
        isContentVisible && visibilityAlphaTitleRow > 0.7f,
        enter = expandVertically(expandFrom = Alignment.Top),
    ) {
        YourAlphaComposable(modifier = Modifier.alpha(visibilityAlpha))
    }

    ChainingAnimationLaunchedEffect(
        isVisible,
        animatedRadius,
        radius,
        animatedAlphaTitle,
        visibilityAlphaTitleRow,
        animatedAlpha,
        visibilityAlpha
    )
}

@Composable
private fun ChainingAnimationLaunchedEffect(
    isVisible: MutableState<Boolean>,
    animatedRadius: Animatable<Float, AnimationVector1D>,
    radius: Float,
    animatedAlphaTitle: Animatable<Float, AnimationVector1D>,
    visibilityAlphaTitleRow: Float,
    animatedAlpha: Animatable<Float, AnimationVector1D>,
    visibilityAlpha: Float
) {
    var radius1 = radius
    var visibilityAlphaTitleRow1 = visibilityAlphaTitleRow
    var visibilityAlpha1 = visibilityAlpha
    if (!isVisible.value) {
        LaunchedEffect(!isVisible.value) { isVisible.value = true }
    }

    if (isVisible.value) {
        LaunchedEffect(isVisible.value) {
            animatedRadius.animateTo(maxRadiusPx, animationSpec = tween()) { radius1 = value }
            delay(100L)
        }
    }

    if (radius1 >= (maxRadiusPx * 0.825f)) {
        LaunchedEffect(radius1 >= (maxRadiusPx * 0.8f)) {
            animatedAlphaTitle.animateTo(1f, animationSpec = tween()) {
                visibilityAlphaTitleRow1 = value
            }
        }
    }

    if (radius1 == maxRadiusPx && visibilityAlphaTitleRow1 == 1f) {
        LaunchedEffect(radius1 == maxRadiusPx && visibilityAlphaTitleRow1 == 1f) {
            delay(150L)
            animatedAlpha.animateTo(1f, animationSpec = tween()) { visibilityAlpha1 = value }
        }
    }
}

                    
```
