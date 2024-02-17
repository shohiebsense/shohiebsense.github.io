Just want to make things easier, by keeping things in mind that the possible steps are:

1. Adjusting Which Flutter SDK **AND** Dart SDK version that we would take.
2. Adjusting the Kotlin version that we would take.

the 'how to' is that you can find on the internet. I just want to wrap things up. It's scattered and has potential oblivion.  

Have a look at Flutter SDK Release, which Flutter And Dart Versions are: 

[Flutter SDK Archive](https://docs.flutter.dev/release/archive?tab=macos)  

Then take a look at your `pubspec.yaml` on the environment, say it has `sdk: '>=3.3.0 <4.0.0'` then you can see which dart version, precisely, which flutter version has the right dart sdk version for your compiler.  

next you go to the flutter sdk path on your machine. Then `git checkout <version>` it  

for example I'm choosing 3.7.12 so `git checkout 3.7.12`  

Then there you go, you can `pub get` the project.  

You also potentially can have the gradle version issue, which the cause is in which version is your kotlin compiler.(?)   

So just go to the project level of `build.gradle` then adjust the kotlin version accordingly.  

Usually the older version has the app dependency like this on the app level of `build.gradle`  

```gradle
implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk7:$kotlin_version"
```

