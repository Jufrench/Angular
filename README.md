# Angular
---------
## MVVM

#### Design Patterns
  * Well documented solution to a recurring problem (architectural pattern)
  * *Gang of four: Design Patterns: Elements of Reusable Object-Oriented Software*

### MVC Framework

#### Model
* Manages the behavior & data of the app domain
* Responds to requests for information about its state (usually from the view)
* Responds to instructions to change state (usually from the controller)
* In event-driven systems, the model notifies observers (usually views) when the information changes so they can react
  * When the model is updated the views will be automatically triggered to update themselves based on the change to the model state

#### View
* Renders the model into a form suitable for interaction, typically a user interface element
* Multiple views can exist for a single model for different purposes
* A viewport typically has a one to one correspondence w/ a display surface and knows how to render to it

#### Controller
* Receives user input & initiates a response by making calls on model objects
* A controller accepts inputs from the user and instructs the model & viewport to perform actions based on that input
* The controller causes the change of the state of the model after it accepts input
* May also cause the view to change the way it's showing information

### Model View View-Model (MVVM)
* Descendent of MVC
* Sometimes called Model-View-Binder
* View model
  * Abstraction of the view that exposes public properties & commands
------
## Services

* Component classes should be kept lean
  * Fetching data from server, user input validation, & logging should be delegated to a service
  * Mainly act as a mediator between the view & app logic (between view & model)
  * Provides view-model like ability to component
  * Component classes can leverage the work of a *Service* to get their work done
* Try to factor out the app logic into services & let them do the heavy lifting
  * Dependency Injection
  * Communicate w/ the server
  * Input validation
* Service gets injected into the component to provide features that the component can then use

#### Angular Service Basics
  * Create service
    * ng generate service + services/serviceName
    * 2 files get created
      * **src/app/services/fooPath.service.spec.ts**
        * Using for testing Angular service
      * **src/app/services/fooPath.service.ts**
        * Where we'll create the fooName service & inject it into the app module & make use of it in the main component
    * To make the service injectable into other components:
      ```
      import { Injectable } from '@angular/core';
      @Injectable()
      export class FooService {

        constructor() {}

      }
      ```
    * Now we configure the service to provide information:
      * Import the service into the main **app.module.ts** in the ngModule decorator, as a **provider**.
      * When imported, it also needs to be passed as a parameter in a constructor of a class, like so:
        ```
        constructor(private fooService: FooService) {}
        ```

---

### Dependency Injection

* Software design pattern that implements inversion o
* One object is dependent on another object
* Four rules:
  1. The Service
    * Needs to be injected
  2. The Client
    * Dependent upon the service(the component)
  3. The Interfaces
    * Once injected, how do you make use of the service
  4. The Injector
    * The entity that is responsible for injecting the object into another object

###### Angular and DI
  * Separation of business logic & dependency construction
  * The dependency is passed to the object consuming it where it is needed
  * Angular injector subsystem is responsible for:
    * Creating components
    * Resolving their dependencies
    * Providing them to other components
##### Dependency
  * Your object is dependent on another object
  * An object that ca be used (a service)
  * 3 ways to access another object:
    1. Create dependency/object itself by using **new** operator
    2. Look up dependency using a global variable
    3. Have dependency passed to it where needed
    * Third option is most flexible because the object is being injected wherever you need it.
    * Testing becomes feasible
      * You could create mock objects

##### Injection
  * Passing the dependency to a dependent object
  * Taking an object and making it available to another object, so that the 2nd object can use some of its mechanisms
  * The client doesn't need to build the object
