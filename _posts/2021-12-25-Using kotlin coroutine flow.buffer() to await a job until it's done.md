https://www.youtube.com/watch?v=B_3iTVJT8Zs&t=209s \

Suppose there's a job, a heavy one, being executed but the user wants to interact with components.
There will be some abrupt come out.

Kotlin coroutine's flow can handle this thing.

```kotlin
@Composable
fun Greeting(name: String) {
    val text = remember { mutableStateOf("Hello $name") }
    var aaa by remember { mutableStateOf(0) }
    val isEmitting = remember { mutableStateOf(false) }
    val processFlow = remember {
        flow {
            if (!isEmitting.value)
                isEmitting.value = true
            else
                return@flow

            delay(2000L)
            aaa++
            emit("aaaaa $aaa")
            isEmitting.value = false
        }
    }
    val coroutineScope = rememberCoroutineScope()
    Column {
        Text(text = text.value)
        Button(onClick = {
            coroutineScope.launch {
                processFlow.buffer().collect {
                    Log.e("emitted ", it)
                    text.value = it
                }
            }
        }) {

        }
    }
}
```

In action: \
I do rapid clicking, to make sure the process inside prevents it

![action](https://github.com/shohiebsense/shohiebsense.github.io/blob/master/Record_2021_12_25_16_13_08_228.gif)
