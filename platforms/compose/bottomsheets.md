# BottomSheets

<figure><img src="../../.gitbook/assets/3.png" alt=""><figcaption></figcaption></figure>

To create a Dialog class, you should inherit it from `BottomSheetCompose` from the [bootstrap](https://github.com/AlexExiv/Router-Android/blob/main/compose/src/main/java/com/speakerboxlite/router/compose/bootstrap/BaseViewCompose.kt) package.

```kotlin

class BottomSheetView: BottomSheetCompose()
{
    @Composable
    override fun Root()
    {
        BottomSheet()
    }
}

@Composable
fun BottomSheet()
{
    // content of BottomSheet
}
```
