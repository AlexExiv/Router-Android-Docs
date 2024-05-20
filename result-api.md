# Result API

An easy and convenient way to obtain results from the called screen. To use it, the called path should implement the `RoutePathResult<Result>` interface, where `Result` is the type of the returning value. Then, in code, simply call the `routeWithResult` method. The first parameter is a reference to the ViewResult subclass, and the second is the path to which you want to navigate. ViewResult subclasses are Fragments and ViewModels that implement the ViewResult interface.

```kotlin
router.routeWithResult(this, ScreenPath()) { 
    /* handle result here */
    
    it.vr // reference to the object passed to the method
    it.result // result
    it.vr.onHandleResult(it.result)
}
```

In the result closure, you receive a data structure that has a reference to the ViewResult subclass passed to the method and the result of the called screen's job.

**Important:** why do we pass the ViewResult to the `routeWithResult` method? Why don't we use `this` context of the ViewModel in the closure? It's because the Fragment or ViewModel could be recreated by the system by the time you get the result in the closure. Therefore, the Result API returns to you a fresh reference to the Fragment or ViewModel.

**Chains case:** Result from a screen that is part of a chain is delivered to the caller of the chain.
