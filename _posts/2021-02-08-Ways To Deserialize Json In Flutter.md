Have a look at [here](https://flutter.dev/docs/development/data-and-backend/json) first.  
Say you got this type of .json

<pre>
{
  "Message": "72",
  "Result": 200,
  "data": [
    {
      "id": 53,
      "name": "Sebastian Michaelis",
      "url": "http://sebastianmichaelis.com",
      "desc": "Dabesto Numero Uno.",
      "pic": "aws.com/cute_sebastian.png"
    },
    {}
  ]
}
</pre>

Import necessary libraries.

```
import  'package:http/http.dart'  as http;
import  'dart:convert';

Future<BaseModel> getData(String url, BaseModel baseModel) async {
    final response = await http.get(url);
}

```

Then there you go.

## #1. Accessing Through Keys

<pre>  
Map<String, dynamic> list = json.decode(response.body);  
List<dynamic> data = list['data'];

data.forEach((element) {
    print(element['name']);
});
</pre>

Accessing The Element/Item

<pre>
var data= list["data"];
var item = data[0];

int id = item["id"];
String name = item["name"];
String desc = item["desc"];
String url = item["url"];
String pic = item["pic"];
</pre>

## 2. Mapping To The Model Like You Did In Serialization-Deserialization Library

Yeah.

<pre>
class AnimeChar {
  final int id;
  final String name;
  final String desc;
  final String url;
  final String pic;

  AnimeChar({this.id, this.name, this.url, this.pic});

  AnimeChar.fromJson(Map<String, dynamic> json) :
    id = json["id"];
    name = json["name"];
    desc = json["desc"];
    url = json["url"];
    pic = json["pic"];

}

</pre>

Here goes the way.

<pre>  
Iterable data = list['data'];  
List<AnimeChar> animeCharList = List<AnimeChar>.from(data.map((e) => AnimeChar.json(e)));  
</pre>
