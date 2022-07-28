1. Know the given string date format, 

2. Make `SimpleDateFormat(THAT_STRING_DATE_FORMAT)`

3. Make `SimpleDateFormat(DESIRED_DATE_FORMAT)`, if you want to change the default language, add `Locale` parameter 
`SimpleDateFormat(DESIRED_DATE_FORMAT, Locale(language = "id", country="ID"))`

4. parse the given string to the desired format to convert string to Date Format  
`givenStringDate = givenStringDateFormat.parse(givenString)`
5. format the the desiredDateFormat
6. `yourDesiredDateFormat.format(givenStringDate)`
  
  
Sample

```kotlin
@SuppressLint("SimpleDateFormat")
fun DateStr.toLoanUIDateFormat() : DateStr {
        val backendTransactionFormat = SimpleDateFormat(DATABASE_TRANSACTION_DATE_TIME_FORMAT)
        val loanDateFormat = SimpleDateFormat(LOAN_UI_DATE_FORMAT, Locale("id", "ID"))
        val date = backendTransactionFormat.parse(this)!!

        return loanDateFormat.format(date)
}
```
