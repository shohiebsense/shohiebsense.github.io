Given the navigation compose libraries

this guy  
`"androidx.navigation:navigation-compose:$nav_version"`  

Has numerous constraints
It uses "/" as the route system so, if you have "/" character on the parameters, you are in trouble.  
Using Parcelable is quite painful.  

The workaround is I would stick to the String, and disregard other primitive types.  
That bunch of parameters you want to bring can be wrapped in to a model.  Make one.  
Join those strings using a separator, for example i use `"---"` separator.  
Every time you found the "/" on your parameter content. Convert it to another, can be anything. For example I use the backslash "\\".  
So your all in one parameter string, can perform this line
```kt 
arg.replace("/", "\\")
```
Then you are good to go. You can send it.
To receive that, unwrap that string inside the bundle just as the navigation compose rule.

```kt
fun Bundle?.getArg(argName: String, defaultValue: String = ""): String {
    if (this == null) return ""
    val value = getString(argName) ?: return defaultValue
    val newValue = revertArgToOriginalValue(value)

    return newValue
}
```

Revert back that "\\" guy. 
```kt
fun revertArgToOriginalValue(arg: String): String {
    return arg.replace("\\", "/")
}
```

Then you can return it back to your made Wrapped Model.  

using the `String.split("---)` it generates an array of string, just map it accordingly.
That's it.

#### When there's an empty argument

Then just use the `String.ifEmpty {"#"}` or whatever the characters except "/"
