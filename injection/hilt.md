# Hilt

## Compose

See [sample-hilt](https://github.com/AlexExiv/Router-Android/tree/main/sample-hilt)

To use Hilt with Compose, you need to add one extra dependency:

```groovy
implementation "com.github.AlexExiv.Router-Android:android-hilt:$version"
```

Also, in RouteController you should use `AndroidHiltViewModelProvider` as ViewModelProvider

```kotlin
typealias RouteControllerApp<Path, VM, V> = RouteControllerVM<Path, VM, AndroidHiltViewModelProvider, V>
```

To get a ViewModel in a Compose view, use the `routerHiltViewModel()` method as shown in the example below:

```kotlin
class MainView: BaseViewCompose()
{
    @Composable
    override fun Root()
    {
        Main(viewModel = routerHiltViewModel())
    }
}

@Composable
fun Main(viewModel: MainViewModel)
{
...
```

If you want to pass parameters to the screen's ViewModel, you should use AssistedInjection in the ViewModel. This allows you to inject dependencies as well as additional parameters when creating the ViewModel. Here's an example:

```kotlin
@HiltViewModel(assistedFactory = StepViewModel.Factory::class)
class StepViewModel @AssistedInject constructor(
    @Assisted val step: Int,
    app: Application): BaseViewModel(app)
{
    @AssistedFactory
    interface Factory
    {
        fun create(step: Int): StepViewModel
    }
    .....
```

Here's an example to illustrate the logic of creating a ViewModel in a `RouteController` using Hilt with AssistedInjection:

```kotlin
class StepPath(val step: Int): RoutePath

@Route
abstract class StepRouteController: RouteControllerApp<StepPath, StepViewModel, StepView>()
{
    override fun onCreateViewModel(modelProvider: AndroidHiltViewModelProvider, path: StepPath): StepViewModel =
        modelProvider.getViewModel { f: StepViewModel.Factory -> f.create(path.step) }
}
```

Full example of AssistedInjection you can find [here](https://github.com/AlexExiv/Router-Android/tree/main/sample-hilt/src/main/java/com/speakerboxlite/router/samplehilt/step)

### Middleware

If you want to use Middleware with injection, you should first obtain the Application Component from Hilt and then pass it to the Router. To do this, modify the App class as shown in the example below:

```kotlin
@HiltAndroidApp
class App: ComposeApplication<RouterComponentImpl>()
{
    lateinit var component: AppComponent // Shared component for the Middleware controllers

    override fun onCreateComponent()
    {
        super.onCreateComponent()
        // Create it like the Hilt's documentation says
        component = EntryPoints.get(this, AppComponent::class.java)
    }

    override fun onCreateRouter()
    {
        routerComponent = RouterComponentImpl()
        routerComponent.initialize(MainPath(), { _, _ -> AnimationControllerComposeSlide() }, component)
    }
}
```
