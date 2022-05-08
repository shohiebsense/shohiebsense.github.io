Right after seeing other apps can show a `.pdf` file on Android, you then wonder how, googling, and stumbled upon the API documentation regarding it:

[`PdfRenderer`](https://developer.android.com/reference/android/graphics/pdf/PdfRenderer)

next, you know something that the idea is to transfer the pdf content on `bitmap`

```java
 public void render(@NonNull Bitmap destination, @Nullable Rect destClip,
                           @Nullable Matrix transform, @RenderMode int renderMode) {

 }
```

The documentation is still not sufficient to get what you want, thus you go to the sample.

[PdfRendererBasic Kotlin](https://github.com/android/graphics-samples/tree/main/PdfRendererBasic)

You get the idea know.

0. Get the file, put in the storage,
1. Open the file using `ParcelFileDescriptor`
2. Initialize the `PdfRenderer`
3. Create a bitmap
4. Send, or render the Pdf Contents to Bitmap
5. `close()` the pdfRenderer including its `renderer.oopenPage` when every content has been rendered

```kotlin
    fun openPage() {
        pdfRenderer?.let { renderer ->
            for (i in 0 until renderer.pageCount) {
                val page = renderer.openPage(i)
                val ratio = page.width.toFloat() / page.height.toFloat()
                val originalBitmap =
                    Bitmap.createBitmap(page.width, page.height, Bitmap.Config.ARGB_8888)
                page.render(originalBitmap, null, null, PdfRenderer.Page.RENDER_MODE_FOR_DISPLAY)
                yourObjectWithOtherParametersList.add(YourObjectWithOtherParameters(bitmap = originalBitmap))
                page.close()
            }
            pdfRenderer!!.close()
        }
    }
```

ok, that's the part one.

the rest is to display the pdf bitmap to UI.

Then you realized  
you need a zoom, a scroll functionality

google it.

or this is [a good repo](https://github.com/umutsoysl/ComposeZoomableImage) to do that

use it, and put it up on `Image` compose.

then you realized again, I want `the next page` functionality using `scrollable` too

1 You need a flag to detect the edge of Pdf Image.  
It can differentiate between scroll of Column/Row and the Image itself.

2. From number 1, you need flags for TopTreshold, RightTreshold, BottomTreshold and LeftTreshold.
3. You need mutable value of `scaleX` and `scaleY`
4. Mind that if the scale is `1` (default), the edge flags are in no need.
5. Enable the Column/Row scrollable when the treshold and the offset is incremental (bigger `offset > x` or smaller `offset < x`) is `true`
6. Mind that `nestedScroll` functionality is required in this one, whether it is `NestedScrollConnection` or other approach.

look up for enable/disable scroll in Column/Row.

or see this [stackoverflow](https://stackoverflow.com/a/69328009)

This is the sample of the idea.

```kotlin
@Composable
fun PdfSection(yourObjectPdfList: List<yourObjectPdf>) {
    val isScrollAllowed = remember { mutableStateOf(false) }

    LazyRow(
        state = listState,
        modifier = Modifier.disabledHorizontal
        putScroll(isScrollAllowed.value)
    ) {
        itemsIndexed(yourObjectPdfList) { index, yourObjectPdf ->
            Box(modifier = Modifier.pointerInput(Unit) {
                forEachGesture {
                    awaitPointerEventScope {
                        awaitFirstDown()
                        do {

                            yourObjectPdf.isXtreshold.value =
                                translationX.absoluteValue == (scaleX / -0.005f).absoluteValue
                            if (yourObjectPdf.isXtreshold.value) {
                                yourObjectPdf.isXtresholdLeft.value =
                                    translationX > 0 &&
                                        translationX.absoluteValue < yourObjectPdf.offsetX.value
                            }

                            if (yourObjectPdf.scale > 1) {
                                if (yourObjectPdf.isXtreshold.value) {
                                    if (yourObjectPdf.isXtresholdLeft.value && offset.x < 0)
                                        yourObjectPdf.offsetX.value += offset.x
                                    else if (!yourObjectPdf.isXtresholdLeft.value && offset.x > 0) {
                                        signPdf.offsetX.value += offset.x
                                    } else if (yourObjectPdf.isXtresholdLeft.value &&
                                            yourObjectPdf.offsetX.value <=
                                                yourObjectPdf.offsetX.value + offset.x
                                    ) {
                                        isScrollAllowed.value = false
                                    } else if (!yourObjectPdf.isXtresholdLeft.value &&
                                            yourObjectPdf.offsetX.value >=
                                                yourObjectPdf.offsetX.value + offset.x
                                    ) {
                                        isScrollAllowed.value = false
                                    }
                                }
                            } else {
                                isScrollAllowed.value = false
                            }
                        } while (event.changes.any { it.pressed })
                    }
                }
            }
        }
    }
}

```

You definitely can do better :)

![Image](https://i.postimg.cc/t4yQvBZc/Record-2022-03-06-22-06-55-408.gif)
