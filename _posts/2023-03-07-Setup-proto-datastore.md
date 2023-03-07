This [documentation](https://developer.android.com/topic/libraries/architecture/datastore) kinda off. 

1.  Go to the [official repo](https://github.com/google/protobuf-gradle-plugin)  
2.  Using the latest version OK  
3.  In `project/app/build.gradle`, add the `dependencies{}`
    ```gradle
    implementation  "com.google.protobuf:protobuf-javalite:3.19.4"
    implementation 'androidx.datastore:datastore:1.0.0'
    ```
4. Make your own `.proto`, read the guide about it [here](https://protobuf.dev/programming-guides/style/)
5. In your `.proto` file, these two lines:
   ```.proto
   option java_package = "com.example.application";
   option java_multiple_files = true;
   ```  
   are important if you want to avoid the unnecessary compile error because of generated java files. Also, adjust your package name accordingly.  
6. Rebuild
7. You should have the generated file under your package: `com.example.application.YourFile`
8. Proceed to make your implemented `Serializer` and dataStore file.
