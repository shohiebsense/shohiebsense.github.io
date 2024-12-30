It's not new but I am here just to convince you.

[https://github.com/google/secrets-gradle-plugin](https://github.com/google/secrets-gradle-plugin)


just add that `buildscript{dependencies{}}}` before plugins on root directory build.gradle.  

then add the plugin.  

You can write variables you want in `local.properties`, build and it will show up.
