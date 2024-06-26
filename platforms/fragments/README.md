# Fragments

## Graddle

#### Project Module

```groovy
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
        ...
    }
}
```

#### App Module

```groovy
implementation "com.github.AlexExiv.Router-Android:router:$version"
implementation "com.github.AlexExiv.Router-Android:annotations:$version"
implementation "com.github.AlexExiv.Router-Android:fragment:$version" // add support of fragments

kapt "com.github.AlexExiv.Router-Android:processor:$version"
```

## Code example

You can find an example project at [sample-fragment](https://github.com/AlexExiv/Router-Android/tree/main/sample-fragment)



### Application

In the first step, we need to configure our \`Application\` class.

Your \`Application\` class should be inherited from the \`FragmentApplication\` class and create and initialize the \`RouterComponentImpl\` in the \`onCreateRouter\` method.

If you're not using Component injection, the App class should look like this:

```kotlin
class App: FragmentApplication<RouterComponentImpl>()
{
    override fun onCreateRouter()
    {
        routerComponent = RouterComponentImpl()
        routerComponent.initialize(MainPath(), { _, _ -> AnimationControllerDefault() })
    }
}
```

Otherwise:

```kotlin
class App: FragmentApplication<RouterComponentImpl>()
{
    lateinit var component: AppComponent

    override fun onCreateComponent()
    {
        super.onCreateComponent()

        component = DaggerAppComponent.builder()
            .appModule(AppModule(AppData("App String")))
            .userModule(UserModule(UserData()))
            .build()
    }

    override fun onCreateRouter()
    {
        routerComponent = RouterComponentImpl()
        routerComponent.initialize(MainPath(), { _, _ -> AnimationControllerDefault() }, component)
    }
}
```

### MainActivity

The second step involves implementing a simple `MainActivity` class. This class should inherit from the `FragmentActivity` class from the [bootstrap](https://github.com/AlexExiv/Router-Android/tree/main/fragment/src/main/java/com/speakerboxlite/router/fragment/bootstrap) package.

Simple `MainActivity` class:

```kotlin
class MainActivity: FragmentActivity(R.layout.activity_main)
```

It's enough if you're using single activity way. Now let's create our first `Fragment`

### SimpleFragment

Your Fragment should be inherited from the Fragment from the [bootstrap](https://github.com/AlexExiv/Router-Android/tree/main/fragment/src/main/java/com/speakerboxlite/router/fragment/bootstrap) package

```kotlin
class SimpleFragment: Fragment(R.layout.fragment_simple)
{
    override fun onViewCreated(view: android.view.View, savedInstanceState: Bundle?)
    {
        super.onViewCreated(view, savedInstanceState)
        arguments // access data
    }
}
```

### SimplePath

Using with class we will navigate to the `SimpleFragment` screen

```kotlin
class SimplePath: RoutePath
```

Now we have to connect `SimplePath` with `SimpleFragment`. In the case of Fragment we have the same way of implementing of RouteControllers and Paths. Look at simple example bellow

```kotlin
@Route
abstract class SimpleRouteController: RouteController<SimplePath, SimpleFragment>()
```

It generates the `onCreateView` method by default if you don't need to pass there extra parameters

Here, we have another example of a simple `RouteController`. In this case, we aim to pass parameters to the screen. When you need to transmit data to your Fragment view, you'll need to implement `onCreateView` yourself and deliver the data to the view using the arguments property.

**Important:** Ensure that the data is serializable to be preserved in the state.

```kotlin
data class SimplePath(val title: String): RoutePath

@Route
class SimpleRouteController: RouteController<SimplePath, SimpleFragment>()
{
    override fun onCreateView(path: SimplePath): SimpleFragment =
        SimpleFragment().apply {
            arguments = Bundle().apply {
                putString("TITLE_KEY", path.title)
            }
        }
}
```

## Code example with ViewModel

Now let's take a look at how `RouteController` looks like when our `Fragment` has a `ViewModel`

### RouteController

When working with ViewModels, it's beneficial to create a `typealias` of `RouteController`

```kotlin
typealias RouteControllerApp<Path, VM, V> = RouteControllerVM<Path, VM, FragmentViewModelProvider, V> // if you don't use Component fo injection
typealias RouteControllerApp<Path, VM, V> = RouteControllerVMC<Path, VM, FragmentViewModelProvider, V, AppComponent> // otherwise
```

If you're not passing arguments to your screen, the definition of `RouteController` remains almost the same, except for adding `SimpleViewModel` to the RouteController.

```kotlin
class SimplePath: RoutePath // The same

// Simple case
@Route
abstract class SimpleRouteController: RouteControllerApp<SimplePath, SimpleViewModel, SimpleFragment>()
```

If you wish to pass arguments, you must override the `onCreateViewModel` method and create the ViewModel as shown in the code below:

```kotlin
class SimplePath(val step: Int): RoutePath // The same

// When you need to pass data to the ViewModel you have to override the onCreateViewModel method
@Route
abstract class SimpleRouteController: RouteControllerApp<SimplePath, SimpleViewModel, SimpleFragment>()
{
    override fun onCreateViewModel(modelProvider: FragmentViewModelProvider, path: SimplePath): SimpleViewModel =
        modelProvider.getViewModel { SimpleViewModel(path.step, it) }
}
```

### SimpleFragment

In this case, we need to inherit our `SimpleFragment` from the `FragmentViewModel` generic class and pass our `ViewModel` as a parameter.&#x20;

The `SimpleFragment` class becomes:

```kotlin
class SimpleFragment: FragmentViewModel<SimpleViewModel>(R.layout.fragment_simple)
{
    override fun onViewCreated(view: android.view.View, savedInstanceState: Bundle?)
    {
        super.onViewCreated(view, savedInstanceState)
        viewModel // will be injected by framework
    }
}
```

### SimpleViewModel

The `SimpleViewModel` class should inherit from the `AndroidViewModel` class provided by the [bootstrap](https://github.com/AlexExiv/Router-Android/tree/main/fragment/src/main/java/com/speakerboxlite/router/fragment/bootstrap) package.

```kotlin
class SimpleViewModel(val step: Int, app: Application): AndroidViewModel(app)
```

It's a good practice to create a `BaseViewModel` class. See example of [BaseViewModel](https://github.com/AlexExiv/Router-Android/blob/main/sample-fragment/src/main/java/com/speakerboxlite/router/sample/base/BaseViewModel.kt)

See other examples here

* [BaseFragment](https://github.com/AlexExiv/Router-Android/blob/main/sample-fragment/src/main/java/com/speakerboxlite/router/sample/base/BaseFragment.kt)
* [SimplePath](https://github.com/AlexExiv/Router-Android/blob/main/sample-fragment/src/main/java/com/speakerboxlite/router/sample/simple/SimplePath.kt)
* [SimpleFragment](https://github.com/AlexExiv/Router-Android/blob/main/sample-fragment/src/main/java/com/speakerboxlite/router/sample/simple/SimpleFragment.kt)

You can find full example of project at [sample-fragment](https://github.com/AlexExiv/Router-Android/tree/main/sample-fragment)



