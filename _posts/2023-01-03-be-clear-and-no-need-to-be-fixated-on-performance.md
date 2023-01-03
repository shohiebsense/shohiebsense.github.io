Consider the problem `Caesar Chiper` coding test, you can google it.

Found the solution like below:
```java
public static String caesarCipher(String s, int k) {
    // Write your code here
        StringBuilder sb = new StringBuilder();
        for (char c : s.toCharArray()){
            if ( c >= 'a' && c<='z'){
                c = (char) ('a' + ( c- 'a' + k) % 26);
            }else if (c >= 'A' && c<='Z'){
                c = (char) ('A' + ( c- 'A' + k) % 26);
            }
            sb.append(c);
        }
        return sb.toString();
    }
```

There's no way, or at least just a tiny possibility to 'remember' it under the real test atmosphere, to me.

This code takes more time to read, moreover, you have to think that you are on a team.

Just be genuine to yourself, if you have some value to uphold, stand by it. If the `performance` bothers you, keep in mind there are so many contexts  
that a product can't bring both `performance` and `flexibility` at the same time.

```kotlin

fun caesarChiper(s: String, k: Int) : String {
    val strBuilder = StringBuilder()
    val lowercaseAlphabet = arrayListOf<Char>()
    val uppercaseAlphabet = arrayListOf<Char>()

    for(char in 'a' .. 'z') {
        lowercaseAlphabet.add(char)
        uppercaseAlphabet.add(char.uppercaseChar())
    }

    s.forEachIndexed { index, it ->
        var char = it
        when (char) {
            in lowercaseAlphabet, in uppercaseAlphabet -> {
                val alphabetCharList = if(it.isUpperCase()) uppercaseAlphabet else lowercaseAlphabet
                val encrypt = (alphabetCharList.indexOf(char)  + k) % 26
                char = alphabetCharList[encrypt]
            }
        }
        strBuilder.append(char)
    }
    return strBuilder.toString()
}

```
