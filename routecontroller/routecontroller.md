# RouteController

Use this type of RouteController if you don't require ViewModel and Component injection. It includes the `onCreateView` method, which is required to be overridden. You can override this method yourself or let the Router do it during code generation. Override this method if you need to pass parameters to the screen.

```kotlin
// Define path to the screen without parameters
class ScreenPath: RouterPath

// Connect the path and screen using RouteController
@Route
abstract class ScreenRouteController: RouteController<ScreenPath, ScreenView>()
```

```kotlin
data class ScreenPath(val title: String): RoutePath

@Route
class ScreenRouteController: RouteController<ScreenPath, ScreenView>()
{
    override fun onCreateView(path: ScreenPath): ScreenView = // logic of creating of the Screen and pass params to it
}
```
