# BottomSheets

Like with Dialogs, the Router doesn't have a special method like `router.routerBTS(...)` to navigate to a BottomSheet, as this would break the project's philosophy. The caller shouldn't know what it is calling; it only navigates by Path. Therefore, your BottomSheet screen should implement the `ViewBTS` interface to inform the Router that this screen is a BottomSheet. This means that only the Screen knows that it is a BottomSheet and knows how to present itself.

In practice, you don't need to implement the `ViewBTS` interface yourself. You can use predefined classes available in the Fragment [bootstrap](https://github.com/AlexExiv/Router-Android/blob/main/fragment/src/main/java/com/speakerboxlite/router/fragment/bootstrap/BottomSheetDialogFragment.kt) package and Compose [bootstrap](https://github.com/AlexExiv/Router-Android/tree/main/compose/src/main/java/com/speakerboxlite/router/compose/bootstrap) package.

### Implementation

You can read more about implementing BottomSheets in the [Fragment](../platforms/fragments/bottomsheets.md) and [Compose](../platforms/compose/bottomsheets.md) sections.&#x20;

Additionally, since BottomSheets usually send results, refer to the [ResultApi](../result-api.md) section for more information.



