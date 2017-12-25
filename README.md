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

------
## Angular @NgModule

##### declarations (mainly components) (array): (views) the classes displaying data
  * Here you'll list your components whether they're Angular inherit components or ones you've created yourself.
##### imports (array)
  * Here you'll list your modules that you'll need, whether they're Angular inherit or modules that you've created yourself.
##### providers (services) (array): (models) the classes getting and handling data
  * Here you'll list your services.
##### bootstrap (array)
------

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

* **A way to supply a new instance of a class with the fully-formed dependencies it requires.**
* **Most dependencies are services.**
* Software design pattern that implements inversion o
* One object is dependent on another object
* **Services are made available to components through DI**
* Angular uses dependency injection to provide new components with the service they need.
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

###### Injection
  * Passing the dependency to a dependent object
  * Taking an object and making it available to another object, so that the 2nd object can use some of its mechanisms
  * The client doesn't need to build the object

###### Angular can tell which services a component needs by looking at the types of its constructor parameters. For example, the constructor for a ```HeroListComponent``` needs a ```HeroService```:

```
constructor(private service: HeroService) {}
```
  * When Angular creates a component, it first asks an **injector** for the services that the component requires.
  * An injector maintains a container of service instances that it has previously created.
  * If  requested service instance is not in the container, the injector makes one and adds it to the container before returning the service to Angular.
  * When all requested services have been resolved & returned, Angular can call the component's constructor with those services as arguments --> Dependency Injection

  * Injectors know to make services (if it doesn't already have a service) because it should have been previously registered as a **provider**.
  * **A provider is something that can create or return a service (typically the service class itself)**
  * You can register providers in modules or components but generally they're added to the **root module** so that the same instance of a service is available everywhere.

#### How to Create a Service
  * Create a service.
  * Inject it into your application.
  * Use it in your components.

 **Adding a Service**
  1. Create a folder named *services*
  2. Add a service to the application with the Angular CLI.
    * Type the following in the prompt:

      ``` ng generate service services/serviceName
      ```
    * 2 new files will be created in the *services* folder
      * serviceName.service.ts
      * serviceName.service.spec.ts
    * In the serviceName.service.ts file add:

      ```
      import { Injectable } from '@angular/core';
      ```
      ```
      @Injectable()
      export class ServiceName {...
          }
      ```
    * Add the service to the app.module.ts file:
      ```
      import { ServiceNameService } from './services/serviceName/service';
      @NgModule({
        ...
        providers: [ServiceName],
        ...
        })
        ```
    **Using the Service**

      * Update componentName.component.ts file to make use of the service:

      ```
      import { ServiceName } from '../services/serviceName.service';

      export class ComponentName {
        constructor(private serviceName: ServiceName) { }
      }
      ```
------

## Generate a Header/Footer

  * ng g or ng generate component header
    * Angular CLI adds to the app.module file the following:
    ```
    import { HeaderComponent } from './header/header.component';
    ```
    * Also adds *HeaderComponent* to declarations array in @NgModule
  * Add to your app.component.html file:
  ```
  <app-header></app-header>
  <app-footer></app-footer>
  ```
-------

------
## Routing
  * Enable navigation among views
  * Uses a browser URL as an instruction to navigate among various client-generated views
    * Can also pass along optional parameters among different views.
  * Angular router leverages HTML5 history manipulation to modify the browser URL.

###### HTML5 History API
* Gives developers the ability to modify a website's URL without a full page refresh
* HTML5 History API Methods:
  * **pushState()**: Add history entry
  * **replaceState()**: Modify history entry
  * Configure ```<base href="/">```

###### Router Terms
* **Router Module**
  * Routes
    * {path: "/home", component: HomeComponent}
    * Allows defining of various routes that Angular Router will use.
* **routerOutlet**
  * Where will the view be rendered in the Angular application?
  * Within the template of the app component, include the following directive:
    * ```<router-outlet></router-outlet>```
* **routerLink**
  * Enables us to specify a path
    * ```<a routerLink="/menu"><Menu</a>```

###### Routing Basics (Instructions)
  * **NOTE**: Consider the button links of a menu bar - Home, About, Contact. Each of these would be supported by using a  **component**.
    * We use the **Angular Router** module to be able to click between the Home, About, and Contact components.


  1. We can use the Angular CLI to create another module.
    * ```ng g module app-routing```
    * Angular creates a bare bones module that has no routing logic. That needs to be added.

  2. Insert into app.module.ts:
    * ```import { AppRoutingModule } from 'path.file';```
    * In the **@NgModule imports** array add ```AppRoutingModule```

  3. Insert into app-routing.module.ts (your routing module).
    * ```import { RouterModule, Routes } from '@angular/router';```
      * This statement is saying that we're going to use the **RouterModule** and the **Routes** module which are inherit in Angular.

  4. Create a ```routes.ts``` file in your routing folder to keep code clean.

  5. Routing syntax
    * ```export const routes: Routes = [
      {path: 'home', component: HomeComponent}
      {path: '', redirectTo: '/home', pathMatch: 'full'}
    ];```
      * Routes is an array.
      * The path is an object.
        * The above syntax says that the path *home* should take you to the corresponding *HomeComponent*.
        * When the URL contains *home*, you'll be navigated to the *HomeComponent*.
      * The default path syntax is the one on the bottom (above)

    6. Import the *routes* constant into the *app-routing.module.ts* file.
      * The *routes* constant will be passed as a parameter in the RouterModule that's in the *imports* array.
        * ```RouterModule.forRoot(routes)```

    7. Make the Router Module available in the global scope by adding ```exports: [ RouterModule ]``` as a property in the *@NgModule*.

    8. How to display the view for a routed path when trying to access a particular component.
      * Angular provides a directive called: ```<router-outlet></router-outlet>```
      * When this tag is used in the template, Angular knows to use it to for the place where the corresponding views needs to be inserted.

    9. Add click functionality to routes (ex: a menu bar with Home, About, Contact)
      * The routing module provides an **attribute directive** thats helps with this called **routerLink**
      * Add the following as an attribute in your **a** tag:
        * ```routerLink='/home'```
