# Middleware

Middleware serves as a tool to intercept navigation between screens under specific conditions. For instance, when a user attempts to navigate to a screen that requires authentication, but the user is not signed in, the Middleware intercepts the navigation and redirects the user to the sign-in screen.

Middleware is created in two steps:

1.  **Create a Middleware Annotation**

    First, create a middleware annotation and mark it with the `@Middleware` annotation:

```kotlin
@Middleware
annotation class MiddlewareSample
```

2.  **Create a Middleware Controller**

    Next, create a Middleware controller by inheriting from `MiddlewareController` or `MiddlewareControllerComponent`. Mark it with the previously created annotation to connect this controller to the annotation:

```kotlin
@MiddlewareSample
class MiddlewareControllerSample: MiddlewareController
```

From this point, you can use your annotation to mark a `RouteController`, indicating that it should call this middleware before navigating to the controller's screen.

```kotlin
@Route
@MiddlewareSample
abstract class SampleRouteController: RouteControllerApp<SamplePath, SampleScreen>()
```

The difference between `MiddlewareController` and `MiddlewareControllerComponent` is that the latter includes the `onInject` method. This method is called after the middleware is created and provides the instance of the component for injection.

```kotlin
@MiddlewareSample
class MiddlewareControllerSample: MiddlewareController
{
    // Implement necessary methods here 
}

@MiddlewareSample
class MiddlewareControllerComponentSample: MiddlewareControllerComponent
{
    override fun onInject(component: Any)
    {
        // Implement injection logic here 
    }
}
```

Full code example:

```kotlin
// Create middleware annotation
@Middleware
annotation class MiddlewareAuth

// Mark MiddlewareController as MiddlewareAuth
@MiddlewareAuth
class MiddlewareControllerAuth: MiddlewareControllerComponent
{
    @Inject
    lateinit var userData: UserData

    // This will be called for injection
    override fun onInject(component: Any)
    {
        (component as AppComponent).inject(this)
    }

    // This method will be called during navigation
    override fun onRoute(router: Router, prev: RoutePath?, next: RouteParamsGen): Boolean
    {
        if (!userData.isLogin.value!!)
        {
            router.route(AuthPath(next))
            return true // return true to block the current navigation 
        }

        return false
    }
}

// Then mark the RouteController as MiddlewareAuth 
@Route
@MiddlewareAuth
abstract class TabAuthRouteController: RouteControllerApp<TabPath2, TabViewModel, TabFragment>()
```
