# Mixed

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
implementation "com.github.AlexExiv.Router-Android:compose:$version" // add support of compose
implementation "com.github.AlexExiv.Router-Android:fragmentcompose:$version" // add support of mixed

kapt "com.github.AlexExiv.Router-Android:processor:$version"
```

## Code example

You can find an example project at [sample-mixed](https://github.com/AlexExiv/Router-Android/tree/main/sample-mixed)

Before reading this section, please make sure to read the sections about [Fragments](fragments.md) and [Compose](compose.md).

### Application

In the first step, we need to configure our `Application` class. Your `Application` class should be inherited from the `ComposeApplication` class and create and initialize the `RouterComponentImpl` in the `onCreateRouter` method.

If you're not using Component injection, the App class should look like this:

```kotlin
class App: MixedApplication<RouterComponentImpl>()
{
    lateinit var component: AppComponent

    override fun onCreateRouter()
    {
        routerComponent = RouterComponentImpl()
        routerComponent.initialize(MainPath(), AnimationFactory(), component)
    }

    override fun provideHostFragmentComposeFactory(): HostFragmentComposeFactory =
        HostFragmentComposeFactoryImpl()
}
```

Otherwise:

```kotlin
class App: MixedApplication<RouterComponentImpl>()
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
        routerComponent.initialize(MainPath(), AnimationFactory(), component)
    }

    override fun provideHostFragmentComposeFactory(): HostFragmentComposeFactory =
        HostFragmentComposeFactoryImpl()
}
```

You need to override the `provideHostFragmentComposeFactory` method to provide a factory that creates the host `Fragment` where the `Router` will display the `Compose` view in the case of Fragment to `Compose` view navigation. Below is an example of the implementation:

```kotlin
class HostFragmentComposeFactoryImpl: HostFragmentComposeFactory
{
    override fun onCreateComposeHostView(): ComposeHostView =
        HostComposeFragment()

    override fun onCreateAnimation(): AnimationControllerFragment<RoutePath, View>? =
        AnimationControllerFragmentDefault()
}
```



