# Dialogs

The Router doesn't have a special method like `router.routerDialog(...)` to navigate to a Dialog, as this would break the project's philosophy. The caller shouldn't know what it is calling; it only navigates by Path. Therefore, your Dialog screen should implement the `ViewDialog` interface to inform the Router that this screen is a Dialog. This means that only the Screen knows that it is a Dialog and knows how to present itself.

In practice, you don't need to implement the `ViewDialog` interface yourself. You can use predefined classes available in the Fragment [bootstrap](https://github.com/AlexExiv/Router-Android/blob/main/fragment/src/main/java/com/speakerboxlite/router/fragment/bootstrap/DialogFragment.kt) package and Compose [bootstrap](https://github.com/AlexExiv/Router-Android/tree/main/compose/src/main/java/com/speakerboxlite/router/compose/bootstrap) package.

### Implementation

You can read more about implementing Dialogs in the [Fragment](../platforms/fragments/dialogs.md) and [Compose](../platforms/compose/dialogs.md) sections.&#x20;

Additionally, since Dialogs usually send results, refer to the [ResultApi](../result-api.md) section for more information.

