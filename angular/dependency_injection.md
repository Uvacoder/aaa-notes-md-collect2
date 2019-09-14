# Dependency Injection

- DI is wired into the Angular framework.

- you can inject a service into a component.

## @Injectable()

- To define a class as a service in Angular, use the `@Injectable() decorator` to provide the metadata that

- An injector creates dependencies, and maintains a container of dependency instances that it reuses if possible.

### Constructor parameter of component

When Angular creates a new instance of a component class it takes the services by looking at the constructor of it

```ts
constructor(private service: HeroService) { }
```

When Angular discovers that a component depends on a service, it first checks if the injector has any existing instances of that service. If not creates a instance of Service registers to the injector and returns the service

## Providing Services

- must register at least one provider of any service you are going to use

### Root level registering of providers

```ts
@Injectable({
 providedIn: 'root',
})
```

When you provide the service at the root level, Angular creates a single, shared instance of HeroService and injects it into any class that asks for it

### Module level registering

you register a provider with a specific NgModule, the same instance of a service is available to all components in that NgModule.

```ts
 @NgModule({
  providers: [
  BackendService,
  Logger
 ],
 ...
})
```

### Component Level Registering

you get a new instance of the service with each new instance of that component.

```ts
@Component({
  selector:    'app-hero-list',
  templateUrl: './hero-list.component.html',
  providers:  [ HeroService ]
})
```
