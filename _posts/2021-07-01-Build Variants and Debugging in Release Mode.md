https://developer.android.com/studio/build/build-variants

https://stackoverflow.com/questions/27321979/generating-unsigned-release-apk-with-android-studio

https://stackoverflow.com/questions/25001479/app-release-unsigned-apk-is-not-signed


By default Android Studio provides two build types / build variants; debug and release.  

You can make the others too.  

Why Build Variants?

- 'Same', or 'Similar' Codes, different characteristics displayed to users
- Different API Key for staging/debug and production/release
- No need to chanage the configurations prior the build, even for the various target SDK

Why Debugging in Release Mode

- No need to manually do copying the .apk file to the device.

How to 

1. (Sign your app with your key)[https://developer.android.com/studio/publish/app-signing#sign_release]  
you can use (KeyStore Explorer)[https://keystore-explorer.org/]

2. ```Android Studio -> View -> Tool Windows -> Build Variants``` or Click ```Build Variants``` on the left bottom 
3. Change the ```Active Build variant``` to ```Release```
4. File -> Project Structure -> Choose Build Variants
5. You can change the ```Signing Config```
6. In ```Modules``` You can change the configurations there, like set the ```Debuggable``` to ```true```
7. In ```Signing Configs``` add the generated keystore to it.
8. Locate the ```app/src```
9. Add the default Build Types ```debug``` and ```release```
10. Say you want to have different String value from xml. add the xml to the ```res/values/yourfilename.xml```
11. Same goes to the other one
12. The final stage is, you both have the same file(s), same path, in different parent folder
```debug/res/values/yourfilename.xml``` and ```release/res/values/yourfilename.xml```
13. Rebuild if it is needed and Run the app.
