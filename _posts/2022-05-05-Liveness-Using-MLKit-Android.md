Integrate with CameraX by adding `ImageAnalysis.Analyzer` when build `ImageAnalysis`

```

val cameraExecutors = Executors.newSingleThreadExecutor()

ImageAnalysis.Builder()
            .setTargetRotation(Surface.ROTATION_0)
            .build()
            .also { imageAnalysis ->
                imageAnalysis.setAnalyzer(
                    cameraExecutors,
                    getCameraXAnalyzeManager(
                        frameHandler,
                        coroutineScope
                    )
                )
            }
```

get the image from this overriden function

```
 override fun analyze(image: ImageProxy) {
          imageProxy.image?.let { it ->

            val image: InputImage = InputImage.fromMediaImage(
                it,
                imageProxy.imageInfo.rotationDegrees
            )
       }

       detector.process(image)
       ...
    }
```

Read [this](https://developers.google.com/ml-kit/vision/face-detection/face-detection-concepts)

Then you learned what attributes that you can get

```
1. tracking Id
2. headEulerAngleX
3. headEulerAngleY
4. headEulerAngleZ
5. boundingBox
6. smileProbability
7. rightEyeOpenProbability
8. leftEyeOpenProbability
```

it is from

```.java
package com.google.mlkit.vision.face;

```

Read the details [here](https://developers.google.com/android/reference/com/google/mlkit/vision/face/Face)

It produces the value right away after capturing.

Read [this](https://developers.google.com/ml-kit/vision/face-detection/android)

```.kt
val realTimeOpts = FaceDetectorOptions.Builder()
        .setContourMode(FaceDetectorOptions.CONTOUR_MODE_ALL)
        .build()

val detector = FaceDetection.getClient(realTimeOpts)

val result = detector.process(image)
        .addOnSuccessListener { faces ->
            // Task completed successfully
            // ...
        }
        .addOnFailureListener { e ->
            // Task failed with an exception
            // ...
        }
```

`faces` is `List` makes sense, to handle multiple faces during capturing

so you can handle from there.
