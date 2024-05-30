# BottomSheets

<figure><img src="../../.gitbook/assets/3.png" alt=""><figcaption></figcaption></figure>

To create a BottomSheet class, you should inherit it from `BottomSheetDialogFragment` from the [bootstrap](https://github.com/AlexExiv/Router-Android/blob/main/fragment/src/main/java/com/speakerboxlite/router/fragment/bootstrap/BottomSheetDialogFragment.kt) package.

```kotlin
class YesNoBottomSheetFragment: BottomSheetDialogFragment()
{
    // implementation
    // access data in arguments
}
```

Other logic stays the same.

### ViewModel

If you are using a ViewModel, you should inherit `YesNoDialogFragment` from `BottomSheetDialogFragmentViewModel` and pass the ViewModel as a parameter.

```kotlin
class YesNoBottomSheetFragment: BottomSheetDialogFragmentViewModel<YesNoViewModel>()
{
    // implementation
    // access viewModel
}
```

[Full example](https://github.com/AlexExiv/Router-Android/blob/main/sample-fragment/src/main/java/com/speakerboxlite/router/sample/shared/subs/sub1/SharedSub1Fragment.kt)
