# Ways To Deserialize Json In Flutter
Yes.
# Prelude
Say you got this type of .json
```.json
{
  "Message": "72",
  "Result": 200,
  "data": [
    {
      "id": 53,
      "name": "Desi World Radio",
      "url": "http://stream.zenolive.com/4mbfcn4mf24tv",
      "desc": "The Desi World Radio is introducing an internet radio that can access more than 500 Desi radio stations in over 150 countries around the world with no monthly fees.",
      "pic": "url.com/radio_pics/53.png?dt=2515202008:15:14"
    },
    {
      
    }
  ]
}
```
Import necessary libraries.
```.dart
import  'package:http/http.dart'  as http;
import  'dart:convert';

Future<BaseModel> getData(String url, BaseModel baseModel) async {
    final response = await http.get(url);
}
```
Then there you go.

# #1. Accessing Through Keys

```.dart
Map<String, dynamic> list = json.decode(response.body);
List<dynamic> data = list['data'];

data.forEach((element) {
    print(element['name']);
});
```
Accessing The Element/Item
```.dart
var data= list["data"];
var item = data[0];

int id = item["id"];
String name = item["name"];
String desc = item["desc"];
String url = item["url"];
String pic = item["pic"];
```

## 2. Mapping Like You Did In Serialization-Deserialization Library

To Be Continued

