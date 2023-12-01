Recently Flutter released their new version of SDK. One of the biggest changes is null-safety.  

Adjusting your project to them is one of your pains, wait until the change in Android project structure (build.gradle, libraries, manifest, and default Activity)  

Just worry not, you can adjust them by making a sample flutter project through Android Studio  

Then you see changes mainly in build.gradle project level and app level gradle.build. One of them is to adjust the compileversion / target verssion.  

Don't forget to adjust the version of gradle, kotlin, java versions, and the Flutter project version.  

It will ease your anxiety about it.  

Next step is the change mostly about nullsafety, handle build context.
