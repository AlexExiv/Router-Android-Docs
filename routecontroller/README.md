# RouteController

As mentioned before, this class connects `RoutePath`, `Screen`, and serves to implement custom routing logic. It's marked with the `@Route` annotation and implements one of the children of the `RouteControllerInterface`. Currently, we have four predefined RouteController classes:

1. [**Simple RouteController**](routecontroller.md): Supports only Fragment or Compose as the view.
2. [**RouteControllerC**: ](routecontrollerc.md)Supports Fragment or Compose as the view and includes Dagger injection. The letter "C" stands for Component, which is passed to the Controller for injection.
3. [**RouteControllerVM**: ](routecontrollervm.md)Supports Fragment or Compose as the view and includes ViewModel functionality. "VM" stands for ViewModel.
4. [**RouteControllerVMC**:](routecontrollervmc.md) Supports Fragment or Compose as the view, includes ViewModel functionality, and Dagger injection.
