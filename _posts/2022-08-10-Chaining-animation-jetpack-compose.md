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
    
    val radius = remember { mutableStateOf(shapeRadius) }
    val visibilityAlpha = remember { mutableStateOf(0f) }
    val visibilityAlphaTitleRow =remember { mutableStateOf(0f)}
    val isVisibleState = remember { mutableStateOf(false)}


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
                        radius = radius.value
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
    radius: MutableState<Float>,
    animatedAlphaTitle: Animatable<Float, AnimationVector1D>,
    visibilityAlphaTitleRow: MutableState<Float>,
    animatedAlpha: Animatable<Float, AnimationVector1D>,
    visibilityAlpha: MutableState<Float>
) {

    if (!isVisible.value) {
        LaunchedEffect(!isVisible.value) { isVisible.value = true }
    }

    if (isVisible.value) {
        LaunchedEffect(isVisible.value) {
            animatedRadius.animateTo(maxRadiusPx, animationSpec = tween()) { radius.value = value }
            delay(100L)
        }
    }

    if (radius.value >= (maxRadiusPx * 0.825f)) {
        LaunchedEffect(radius.value >= (maxRadiusPx * 0.8f)) {
            animatedAlphaTitle.animateTo(1f, animationSpec = tween()) {
                visibilityAlphaTitleRow1 = value
            }
        }
    }

    if (radius.value == maxRadiusPx && visibilityAlphaTitleRow1 == 1f) {
        LaunchedEffect(radius.value == maxRadiusPx && visibilityAlphaTitleRow1 == 1f) {
            delay(150L)
            animatedAlpha.animateTo(1f, animationSpec = tween()) { visibilityAlpha1 = value }
        }
    }
}

                    
```
