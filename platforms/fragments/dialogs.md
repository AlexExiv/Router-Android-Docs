# Dialogs

To create a Dialog class, you should inherit it from `DialogFragment` from the [bootstrap](https://github.com/AlexExiv/Router-Android/blob/main/fragment/src/main/java/com/speakerboxlite/router/fragment/bootstrap/DialogFragment.kt) package.

```kotlin
class YesNoDialogFragment: DialogFragment()
{
    // implementation
    // access data in arguments
}
```

Other logic stays the same.

### ViewModel

If you are using a ViewModel, you should inherit `YesNoDialogFragment` from `DialogFragmentViewModel` and pass the ViewModel as a parameter.

```kotlin
class YesNoDialogFragment: DialogFragmentViewModel<YesNoViewModel>()
{
    // implementation
    // access viewModel
}
```

[Full example](https://github.com/AlexExiv/Router-Android/blob/main/sample-fragment/src/main/java/com/speakerboxlite/router/sample/dialogs/DialogFragment.kt)
