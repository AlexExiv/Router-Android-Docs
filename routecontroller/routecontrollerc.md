# RouteControllerC

Use this type of RouteController if you don't require a ViewModel but need the application component for injection. It includes the `onCreateView` and `onInject` methods, which are required to be overridden. You can override these methods yourself or let the Router do it during code generation. Override the `onCreateView` method if you need to pass parameters to the screen. Override `onInject` if you have your own method of injection. By default, it generates code like:

```kotlin
protected override fun onInject(view: SimpleComponentScreen, component: AppComponent)
{
    component.inject(view)
}
```

It's a good practice to create typealias for this controller&#x20;

```kotlin
typealias RouteControllerApp<Path, V> = RouteControllerC<Path, V, AppComponent>
```

Where `AppComponent` is a shared application component

```kotlin
// Define path to the screen without parameters
class ScreenPath: RouterPath

// Connect the path and screen using RouteController
@Route
abstract class ScreenRouteController: RouteControllerApp<ScreenPath, ScreenView>()
```

```kotlin
data class ScreenPath(val title: String): RoutePath

@Route
class ScreenRouteController: RouteControllerApp<ScreenPath, ScreenView>()
{
    //@Inject optional if needed
    lateinit var userData: UserData // injected by onInject

    override fun onCreateView(path: ScreenPath): ScreenView = // logic of creating of the Screen and pass params to it
    
    // optional
    override fun onInject(view: ScreenView, component: AppComponent)
    {
        // you custom code to inject dependencies
    }
}
```
