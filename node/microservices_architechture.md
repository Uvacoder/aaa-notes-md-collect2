# MicroService Architechture

https://www.youtube.com/watch?v=gfWr2_H39N0

## Why microServices
### Monolithic Architechture

    - All the components are interconnec
    - ted and interdepended,
    - Tightly coupled software where each componenet along with it's  associtaed components must be present in order to execute or compile the code
    
#### Advantages

    - To scale(more users or more bandwidth) run multiple instances behind a load balancer
    - Simple to develop
    - Easy to deploy as it is a single deployment
#### Disadvantages
##### Large and comple application ,
    - It increasingly difficult the manage the application if it grows large, Because it will be difficult to understand and modify the architechture 
    - As a result development slows down and modularity breaks down.
    - It is difficult to understand how a change will affect
    - So quality of the code decrease
    
##### Slow Development
    - Application and dev team grows it is difficult to understand and modify, 
    - Also slower IDE, which makes less productive
    It is a obstacle to frequenct deployment, Because to change a one componenet redeploying the whole application does't make sense 
    - So it blocks continues development
##### scalable 
    Each copy of the application will access to all of the data, which makes cahing less effective and increase memory consumption. 
    Diffirent application components will have different hardware scopes, Like one will be memory intensive another might be CPU intensive.
    So in monolethic architechture we cannot scale each component independently
    
    
##### Unstable 
    So any bug in a component might bring down entire process or application as the each compenents are interdependent 
    
    So available of the application is low for users
    
##### Inflexible
    Difficult to adopt new framework and languages
    It would extremly expensive to rewrite the completely app to a or new framework even though the new though the new application is considerably better. So there is huge barrier to adopt to new technologies
    

### Microservice Architechture
structures application into collection autonomous moduled around bussiness domain,
all the services communicate through API, each microservice focus one bussiness capability

the microservices communicate between eachother statelessly, which means each request or response is a independent transaction

![](https://i.imgur.com/HHh0VCb.png)

each service can have seperate codebase for each and also seperate development team, so each can be deployed independetly

Because of multiple codebase, each codebase will be small while comparing with monolethic architechture, so in case of rebuilding and deploying becomes easy when a new technology adoptation or simple bug fix,

Also they no need to follow same technology or stack or library etc,


#### Service discoverty
Maintain a list of services and which node they resides,

#### API gateway
Entry point for clients, The client goes to API gateway and the API gateway forward the request particular service

### Features of Microservice architechure
#### small focused

#### loosely coupled

#### languae neutral
Each microservice can follow different architechture

####  Bounded context
Each microservice does't need to understand other microservice 

### Advantages of microservice architechture

- Independent development
- Independent Deploymenet
- Fault Isolation
- Mixed technology stack
- Granular scaling



