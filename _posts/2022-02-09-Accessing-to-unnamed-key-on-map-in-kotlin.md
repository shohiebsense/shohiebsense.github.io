```
{
  "profiles": [
    {
      "data": {
        "id" : 320812381212,
        "name": "Name",
        "email": "email@gmail.com",
        "gender": "Male",
        "custom_personal_attribute": "ehe"
      },
      "type": "personal"
    },
    {
      "data": {
        "id" : 320812381212,
        "name": "asdsad",
        "email": "email@yohaa.com",
        "gender": "Female",
        "custom_spouse_attribute": "aha"
      },
      "type": "spouse"
    }
  ]
}
```

Suppose you don't use `gson` and you iterate using `Map` one by one.  
  
 To get the specific object of `profiles`  
 you can do:
 1. cast the `profiles` as an `ArrayList<Map<String, Any>>`  
 ```val profileList = responseAsMap["profiles"] as ArrayList<Map<String, Any>>```  
 2. filter to get the specific object from the list  
 ```val personalData = profileList.filterList { this["type"] == "personal"}```  
 3. That generates a `List<Map>` data type. Bc you can't figure the `key` out, Iterate that map   
```val personalDataDetail = personalData.listIterator().next["data"] as Map<String. Any```  
  
there you go.
