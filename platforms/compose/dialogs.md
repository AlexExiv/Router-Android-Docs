# Dialogs

To create a Dialog class, you should inherit it from `DialogCompose` from the [bootstrap](https://github.com/AlexExiv/Router-Android/blob/main/compose/src/main/java/com/speakerboxlite/router/compose/bootstrap/BaseViewCompose.kt) package.

```kotlin

class DialogView: DialogCompose()
{
    @Composable
    override fun Root()
    {
        Dialog()
    }
}

@Composable
fun Dialog()
{
    // content of dialog window
}
```
