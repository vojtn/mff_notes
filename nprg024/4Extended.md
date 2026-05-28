| [Overview](./README.md) | [Creational](./1Creational.md) | [Structural](./2Structural.md) | [Behavioral](./3Behavioral.md) | **Extended** | [Relations](./Relations.md)
| - | - | -| - | - | - |

# Extended

## MVC/MVVM

### MVC (Model View Controller)
- original model - 1979
- different concepts

"bridge the gap between the human user's mental model and the digital model that exists in the computer"

#### Motivation
Separation of vizual prezentation, app logic and user control

#### About
Architectural pattern
- can be used with Observer

#### Structure

Model
- keeps the data
- represents the state
- inner logic
- bussiness logika

View
- shows the data to the user
- frontend
- it has data from model
- view - controller 1:1

Controller
- handles user inputs
    -> scrolling (view)
    -> save form data (model)
- can return new view

#### Advantages
- Modularization
- logical composition
- model is independent
- easy to extend

#### Disadvantages
- complex for smaller projects
- view and controller are dependent on each other, on platform or model


### MVVM
- Ken Cooper, Ted Peters – Microsoft, 2005
- WPF = Windows Presentation Foundation
    - declarative design user interface – XAML
    - C# - backend
- data binding


#### Structure

Model
- similar as in MVC
- WPF - C# 

View
- combines View and controller z MVC
- vizual elements - butons, interactive elements
- user inputs

ViewModel
- connection -> databinding
- middleman


#### Advantages
- model indepentent
- easy to test components

#### Disadvantages
- complex design and implementation for smaller projects
- concept complexity


### Related patterns
- Observer
- Adapter
- MVP


## Pipes and filters
An architectural pattern which decomposes a complex problem into small generic tasks, that can then be reused in different problems

### Motivation
Burger stand - hard to handle in one person
 -> mcDonald
- simplifies complex processes

### Structure
Filter
- gets data from a pipe, performs a function -> outputs it to another pipe

Pipe
- transfers and buffers data between filters

Pump
- the source of input for the pipeline
Sink 
- consumes the output

### Usage
- UNIX - pipelines
- Compilers
- Multimedia processing
- Very often -> High-performance computing - independent scalling of individual filters

### Advantages
- flexibility
- filter reusability
- paralelism
- testability
- scalability

### Disadvantages
- error handling
- data transformation overhead
- some

### Related patterns
- Layers
- Competing Consumers

## CQRS + Event Sourcing

### Motivation
tradtional CRUD has limits
-> one model for reading and writing
-> complex bussiness roles often get mixed with persistance
-> current state overwrites the previous state


### CQRS (Command Query Responsible Segregation)
- commands change state
- queries returns data, dosnt change state
-> write and read model can be different
- both can be optimalized and scale independently

### Event-Sourcing
- stores the history of changes (events)
- event are the source of truth
- state reconstruction can be done after a fault


### Command vs Event
Command 
- request to do sth
- can be rejected
- imperative form

Event
- sth that already happened
- cannot be rejected
- pas tense

Together
- Commands produce events
- Events update read models
- Queries read prepared views

### Usage
- e-commerce
- banking and finance
- logistics nad supply chain
- colaborative editing

### Advantages
- clear separation between reads and writes
- full history of changes
- ability to reconstruct the past state
- useful for distributed systems
- easier scaling

### Disadvantages
- more code and infrastructure
- data deletion is harder
- more comples to test and maintain
- not ideal for simple CRUD systems

### Info
- database is  separated - read / write
    - read is way fruquent
- Queries - materialized views for frequent queries

### Related patterns
- Command
- Observer
- Memento
- Repository
- Mediator


## Half-sync/Half-Async
A concurrency pattern for I/O-bound services.

### Motivation
Server with thousands client calls
1. Threads
2. Full Async

Solution
- use async only where speed needed

### Example
- pub:   -> order -> cooks

### Structure

Async Task Layer
- catched the request
- never blocks

Querying Layer
- pending events

Sync Task Layer
- thread pool
- do the actual work


### Usage
- network servers - HTTP, RPC
- OS kernel I/O paths
- I/O bound services with many clients

Real SW
- Apache HTTP Service
- Netty (Java)
- Kafka Consumer

### Advantages
- simplier programming model
- high IO throughput
- clean separation of concerns
- easy unit testing
- independent tuing

### Disadvantages
- overhead
- memory for the queue
- added latency

### Related patterns
- Reactor/Proactor
- Leader/Follower


## Proactor & Reactor

### Motivation
Logging service
- many request at same time -> hard to handle
-> need to structurize

### Reactor

#### Usage
- nginx
- kestrel
- redis
- GUI - WPF, Swing

#### Advantages
- logic separation (app and reactor)
- modularity
- resusability 

#### Disadvantages
- event handling is synchronous
- debugging and testing can be harder

### Proactor
Handles the operations, 

#### Usage
- windows IOCP - SQL server
- io_uring
- async/await in C#

#### Advantages
- modularity
- performance
- easier synchronization

#### Disadvantages
- OS support
- debugging and testing
- planning async operation

### Related patterns
- Half-Sync/Half-Async
- Observer
- Publisher-Subscriber
- Leader/Follower

## Eager/lazy Acquisition

### Lazy acquisition
“Acquire resources at the latest possible time. The resource is not acquired until it becomes unavoidable to do so.”


#### Motivation
Picture archive and communication system

#### Structure

Resource User

Resource Proxy
- access forwarded byt the proxy

Resource provider 
- can work as a factory

Resource

#### Usage
- singleton - lazy evaluation
- operation systems - lazy loading
- Eclipse plug-in - lazy loading
- JIT compilation
- Lazy Evalutaion - Boolean expression, C++, C#

#### Advantages
- stability
- availability
- transparency
- quick start-up

####Disadvantages
- space overhead
- time overhead
- predictability


### Eager acquisition
Eagerly acquire a number of resources before their actual use. At a time before resource use, optimally at start-up. 

#### Motivation
stringent timing nad use about resource acquisition
- How to solve: Acquire the resource early

#### About
- User creates a proxy
- proxy gets the resource

#### Example
- kitchen restaurant - cooks have prepared knives and tools

#### Structure
Proxy

Resource

User

Provider

#### Usage
- AOT compilation
- Poolin

#### Advantages
- predictability
- performance
- flexibility
- transparency

#### Disadvantages
- management responsibility
- static configuration
- over-acquisition
- slow-start-up

| [Overview](./README.md) | [Creational](./1Creational.md) | [Structural](./2Structural.md) | [Behavioral](./3Behavioral.md) | **Extended** | [Relations](./Relations.md)
| - | - | -| - | - | - |