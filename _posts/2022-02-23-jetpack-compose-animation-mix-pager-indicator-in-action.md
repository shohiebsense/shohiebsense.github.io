![AnimatedPagerIndicator](https://i.postimg.cc/L8Lzn4Bv/Record-2022-02-23-13-51-57-304.gif)

The code is [here](https://gist.github.com/shohiebsense/54d8ca16fdfb1b41b343f19de6c1d49a)

Explaination:

```kotlin
 val indicatorWidthPx = LocalDensity.current.run { 8.dp.roundToPx() }
 val spacingPx = LocalDensity.current.run { spacing.roundToPx() }
```

read about it [here](https://stackoverflow.com/questions/65921799/how-to-convert-dp-to-pixels-in-android-jetpack-compose)
converting to px to make the movement less significant

```kotlin
val scrollPosition = (pagerState.currentPage + pagerState.currentPageOffset)
        .coerceIn(
            0f,
            (pagerState.pageCount - 1)
                .coerceAtLeast(0)
                .toFloat()
        )
```

`coerceIn` and `coerceAtLeast` is used to implement `snap` whenever the movement stop on every page.

```kotlin
val value by animateFloatAsState(
    targetValue = if (scrollPosition % 1 == 0F) 8F else 16F,
    animationSpec = spring(
        dampingRatio = Spring.DampingRatioMediumBouncy,
        stiffness = Spring.StiffnessLow
    )
)
```

I use `spring AnimationSpec` so that I can adjust the dampingRatio and stiffness, you can adjust based on your preference.  
Read about it [here](https://developer.android.com/jetpack/compose/animation)

```kotlin
Modifier.offset {
                  IntOffset(
                      x = ((spacingPx + indicatorWidthPx) * scrollPosition).toInt(),
                      y = 0
                  )
              }
  .size(width = value.dp, height = indicatorHeight)
```

`offset` is where the movement is being implemented.  
whereas `size` is the function which you put the value produced from `animateFloatAsState`, put the width parameter with it.
