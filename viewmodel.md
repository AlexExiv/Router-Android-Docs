# ViewModel

In case you use MVVM pattern you have to replace `RouteController` by `RouteControllerVM` or if you use dagger injection by `RouteControllerVMC`

Example of using for the Fragment:

```kotlin
typealias RouteControllerApp<Path, VM, V> = RouteControllerVMC<Path, VM, AndroidViewModelProvider, V, AppComponent>

class TabsPath: RoutePath

// Simple case
@Route
abstract class TabsRouteController: RouteControllerApp<TabsPath, TabsViewModel, TabsFragment>()

class StepPath(val step: Int): RoutePath

// When you need to pass data to the ViewModel you have to override the onCreateViewModel method
@Route
abstract class StepRouteController: RouteControllerApp<StepPath, StepViewModel, StepFragment>()
{
    override fun onCreateViewModel(modelProvider: AndroidViewModelProvider, path: StepPath): StepViewModel =
        modelProvider.getViewModel { StepViewModel(path.step, it) }
}
```



