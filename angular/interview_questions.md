# Interview Questions

## module(ngModule)

[What is module ?](./module.md#module)  
[what is NgModule ?](./module.md#ngmodule)  
[What are the meta data objects properties of @NgModule decorator ?](./module.md#metadata-object)
[What is root component ?](./module.md#root-component)  

## Component

[What is a component in angular ?](./component.md#component)  
[What are the things components comprised of ?](./component.md/#component-is-comprised-of-three-things)  
[How a component recognizes a services ?](./dependency_injection.md#constructor-parameter-of-component)  

## Component Interaction

[What is the use of input and output decorators in component interaction ?](https://angular.io/guide/component-interaction)
[How to pass data from parent to child through input binding ?](https://angular.io/guide/component-interaction#pass-data-from-parent-to-child-with-input-binding)  
[How to intercept the input property with a getter and setter during component interactin ?](https://angular.io/guide/component-interaction#intercept-input-property-changes-with-a-setter)  
[How to intercept the input property with ngOnChanges during component interactin ?](https://angular.io/guide/component-interaction#intercept-input-property-changes-with-ngonchanges)  
[How parent can able to listen events triggered from child ?](https://angular.io/guide/component-interaction#parent-listens-for-child-event)  
[What is the role of eventemitter in component interaction ?](https://angular.io/guide/component-interaction#parent-listens-for-child-event)  
[How Parent component interacting with child component via local variable ( template reference variable ) ?](https://angular.io/guide/component-interaction#parent-interacts-with-child-via-local-variable)  
[How to access child component inside parent component class via local variable ?]([How Parent component interacting with child component via local variable ?](https://angular.io/guide/component-interaction#parent-interacts-with-child-via-local-variable)  
[How to communicate parent and child via services ?](https://angular.io/guide/component-interaction#parent-and-children-communicate-via-a-service)  

## Component styles

[How styles are being added to component ?]()  
[Does the scope of the component styles applied from parent component styles ?]()  
[How to apply style to component host ?]()
[How to apply style to componnet based on component ancesters styles ?]()
[What are the different ways of loading component styles ?]()
[What are the different ways of component view encaptulaztion ?]()

## Dependency injection

[What is dependency injection ?](./dependency_injection.md/#dependency_injection)  
[What a injector does ?](./dependency_injection.md#injectable)  
[What @Injectable() decorator used for ?](./dependency_injection.md#injectable)  
[What are the providers involvement in component ?](./dependency_injection.md#providing-services)

## Services

[What are services ?](./services.md#services)  
[What are three levels of registering of services ?](./dependency_injection.md#providing-services)

## http client module

[What is http client module ?](./http.md#http)  
[How HttpClient.get works ?](./angular/http.md#httpclientget)  
[How HttpClient Error handler works ?](./)

## Router

[What is routing ?](./routing.md#routing)  
[What is RouterModule ?](./routing.md#RouterModule.routermoduleforroot)  
[What are route properties ?](./routing.md#route-properties)  
[What RouterModule.forRoot function does ?](./routing.md#note--forroot)  
[What is router outlet ?](./routing.md#router-outlet)  
[What is router link in component template ?](./routing.md##router-link--navigation-link-)  
[What is activated Route ?](routing.md#activated-route--using-route-information-)  
[How to make routing as a seperate module and include it with root module ?](./routing.md#app-routing-module)

## Template syntax

[What is interpolation ?](./template_syntax.md#template-syntax)  
[What are the ways of binding ?](./template_syntax.md#three-ways-of-data-binding-in-angular)  
[How attribute binding and DOM property works ?](./template_syntax.md#html-attribute-binding)  
[Difference between property binding and interpolation ?](./template_syntax.md#property-binding-vs-interpolation)  
[Content security of interpolation and property binding ?](./template_syntax.md#content-security)  
[What is attribute binding ?](./template_syntax.md#attribute-binding)  
[What is class binding ?](./template_syntax.md#class-binding)  
[What is event binding ?](./template_syntax.md#class-binding)  
[What are custom Events ?](./template_syntax.md#customevents)  
[What are some of the built-in directives ?](./template_syntax.md#built-in-directives)  
[How NgClass directive workds ?](./template_syntax.md#ngclass)  
[How NgStyle directive workds ?](./template_syntax.md#ngstyle)  
[How NgModel directive workds ?](./template_syntax.md#ngmodel)  
[How NgSwitch directive workds ?](./template_syntax.md#ngswitch)  
[What are template binding variable ?](./template_syntax.md#template-reference-variables-var)  
[Input decorator and output decorator ?](./template_syntax.md#input-and-output-properties)  
[What is Template expression Operators ?](./template_syntax.md#template-expression-operators)  
[What is pipe operator ?](./template_syntax.md#the-pipe-operator---)  
[What is safe navigation operator ?](./template_syntax.md#safe-navigation-operator---)  
[what is non-null operator ?](./template_syntax.md#the-non-null-assertion-operator---)  
[What is build type cast function ?](./template_syntax.md#build-in-template-functions)  

## Angular lifehooks

[What are lifecycle hooks ?](./componenet_life_cyle_hooks.md#component-lifecycle-hooks)  
[What is lifecycle interface ?](./componenet_life_cyle_hooks.md#lifecycle-interface)  
[Is it mandatory to use interfaces when using lifecycle hooks?](./componenet_life_cyle_hooks.md#is-interfaces-required-for-life-cycle-events)  
[What is the purpose of using lifecycle interfaces ?](./componenet_life_cyle_hooks.md#is-interfaces-required-for-life-cycle-events)  
[What is the first lifecycle hook which will get invoked ?](./componenet_life_cyle_hooks.md#ngonchanges)  
[What is the purpose of ngOnChanges and when it will be invoked ?](./componenet_life_cyle_hooks.md#ngonchanges)  
[What is the purpose of ngOnInit and when it will be invoked ?](./componenet_life_cyle_hooks.md#ngoninit)  
[Why we need to use constructor as well as ngInit ?](./componenet_life_cyle_hooks.md#constructor-vs-ngoninit)
[What is the purpose of ngDoCheck and when it will be invoked ?](./componenet_life_cyle_hooks.md#ngdocheck)  
[What is the purpose of ngAfterContentInit and when it will be invoked ?](./componenet_life_cyle_hooks.md#ngaftercontentinit)  
[What is the purpose of ngAfterContentChecked and when it will be invoked ?](./componenet_life_cyle_hooks.md#ngaftercontentchecked)  
[What is the purpose of ngAfterViewInit and when it will be invoked ?](./componenet_life_cyle_hooks.md#ngafterviewinit)  
[What is the purpose of ngAfterViewChecked and when it will be invoked ?](./componenet_life_cyle_hooks.md#ngafterviewchecked)  
[What is the purpose of ngOnDestroy and when it will be invoked ?](./componenet_life_cyle_hooks.md#ngondestroy)  

