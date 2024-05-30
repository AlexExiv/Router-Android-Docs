# Tabs

<figure><img src="../.gitbook/assets/1.png" alt=""><figcaption><p>Tabs screen</p></figcaption></figure>

To create tabs, you need to mark the `RouteController` with the `@Tabs` annotation, as shown in the example below:

```kotlin
class TabsPath: RoutePath

@Tabs
@Route
abstract class TabsRouteController: RouteController<TabsPath, TabsView>()
```

It’s important to note that a screen can have only one tabs hoster.

The `@Tabs` annotation has three parameters:

1. **tabRouteInParent**: If `true`, calling the `route(..)` method inside the tab will show a new screen above the tabs. Default value is `false`
2. **backToFirst**: If `true`, calling the `back()` method, when the current tab's stack has only one screen, will switch the selected tab to the first tab. If the `back()` method is called while on the first tab, it will lead to closing the tabs screen. Default value is `true`
3. **tabUnique**: Defines how the uniqueness of the tab's path will be determined. Default value is `TabUnique.Class.` Available values are `TabUnique.None, TabUnique.Class, TabUnique.Equal`

### Important route behaviour

Why do we need the tab's path to be unique? To answer this question, you first need to understand how navigation works inside a screen.

As we remember, the philosophy of the Router tells us that a screen shouldn't know how to show the next screen or how navigation should be executed. In other words, we can't do something like this:

```kotlin
(parentFragment as TabsFragment).changeTab(0)
//or
App.shared.mainActivity.changeTab(0)
//or whatever it is
```

Instead, navigation should be handled in a way that the screen only knows it needs to navigate, but not the specifics of how that navigation is performed. This keeps the business logic separate from the navigation logic, maintaining a clean architecture.

When you call `router.route(...)`, the Router will first try to find this path among all tabs' root screens in the stack. If it finds the path, it will close all screens above the tab screen that contains this path, then change the current tab in the tab screen, and close all screens in the stack of this tab. Therefore, we need to tell the Router how it can compare paths:

* **TabUnique.None**: Don't search for the path in the tree.
* **TabUnique.Class**: Compare classes.
* **TabUnique.Equal**: Call the `equals` method to compare them.

### Implementation

You can read more about implementing Tabs in the [Fragment](../platforms/fragments/tabs.md) and [Compose](../platforms/compose/tabs.md) sections.
