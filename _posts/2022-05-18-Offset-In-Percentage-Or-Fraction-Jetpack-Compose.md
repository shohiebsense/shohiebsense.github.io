Consider this problem  

[Align Composables on all the edges of the screen while rotated](https://stackoverflow.com/questions/70455757/align-composables-on-all-the-edges-of-the-screen-while-rotated)  

Well, try with the longer text.  

Then you realize it's no longer centered.  

You can however use `Modifier.offset()` with `double` value.  

What about using fraction or Percentage.  

For example it is for `CenterEnd` Alignment

```kotlin
Modifier.layout { measurable, constraints ->
                                val text = measurable.measure(constraints)
                                layout(text.height, text.width) {
                                    text.place(text.width, 0)
                                }
                            }
```

tadaaa

