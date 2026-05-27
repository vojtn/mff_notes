
# Factory Method and Template Method
Factory Method is a specialization of Template Method. At the same time, a Factory Method may serve as a step in a large Template Method.

# Factory Method and 
Many designs start by using Factory Method (less complicated and more customizable via subclasses) and evolve toward Abstract Factory, Prototype, or Builder (more flexible, but more complicated).

# Factory Method and Prototype
Prototype isn’t based on inheritance, so it doesn’t have its drawbacks. On the other hand, Prototype requires a complicated initialization of the cloned object. Factory Method is based on inheritance but doesn’t require an initialization step.

# Abstract Factory and Factory method
Abstract Factory classes are often based on a set of Factory Methods, but you can also use Prototype to compose the methods on these classes.

# Abstract Factory and Builder
- builder - step by step, speration of construction process from representation
Abstract Factory specializes in creating families of related objects. Abstract Factory returns the product immediately, whereas Builder lets you run some additional construction steps before fetching the product.

# Abstract Factory and Singleton
Abstract Factory can be implemented as a singleton

# Builder and Composite
You can use Builder when creating complex Composite trees because you can program its construction steps to work recursivel


# Builder and Prototype 
Builder may use prototypes to initialize parts

# Builder and Singleton
Builder can be implemented as singleton.

# Builder and Bridge
Can be combined together. Director class -> abstraction and differnt builders can acts as implementations.

# Prototype and Singleton
Prototype can be implemented as singleton

# Prototype and Composite
Designs that make heavy use of Composite and Decorator can often benefit from using Prototype. Applying the pattern lets you clone complex structures instead of re-constructing them from scratch.

# Prototype and Abstract Factory
Abstract Factory classes are often based on a set of Factory Methods, but you can also use Prototype to compose the methods on these classes.

# Prototype and Command
Prototype can help when you need to save copies of Commands into history.

# Abstract Factory and Singleton
Abstrct factory can be implemented as singleton.

# Singleton and Facade
Facade class can often be transformed into a Singleton since a single facade object is sufficient in most case

# Proxy and Facade
- both add and new layer betwen the client and system
- Facade add a simplified interface
- Proxy provides the same interface, its interchangeble with its service object

# Proxy and Adapter
- With Adapter you access an existing object via different interface. 
- With Proxy, the interface stays the same.

# Proxy and Decorator
They have similar structures, but very different intents/implementation. Both patterns are built on the composition principle, where one object is supposed to delegate some of the work to another. 
The difference is that a Proxy usually manages the life cycle of its service object on its own, whereas the composition of Decorators is always controlled by the client and the decorator adds some properties to the object.

# Facade and Adapter
Dases is similar to object adapter, however it has differnet purpose. Facade simplified behaviour of complex subsystems, it defines new iterface for existing objects. However Adapter solves the intercompatibility, it tries to make the existing interface usable, it usually wraps just one object.


# Facade and Mediator
Both have similar jobs - organizing collaboration between lots of classes.
Mediator hides complexity between subsystems objects themselves, however the Facade hides the complexity from the client.


# Facade and Abstract factory
Abstract Factory can serve as an alternative to Facade when you only want to hide the way the subsystem objects are created from the client code.

# Facade and Flyweight
Flyweight shows how to make lots of little objects, whereas Facade shows how to make a single object that represents an entire subsystem.

# Adapter and Decorator
Adapter provides a completely different interface for accessing an existing object. On the other hand, with the Decorator pattern the interface either stays the same or gets extended. In addition, Decorator supports recursive composition, which isn’t possible when you use Adapter.

# Adapter and Bridge
They solve the same problem, the adaption some code, but the time usage is differnt. We use adapter, when we need to solve integrate into existing code.  is commonly used with an existing app to make some otherwise-incompatible classes work together nicely.
However Bridge is usually designed up-front, letting you develop parts of an application independently of each other.



# Bridge and Abstract factory
Cna be used together.
This pairing is useful when some abstractions defined by Bridge can only work with specific implementations. In this case, Abstract Factory can encapsulate these relations and hide the complexity from the client code.

# Bridge and Strategy
Also based on composition and delegate the work but solves different problems.
Strategy can choose the implementation in runtime



# Composite and Decorator
Composite and Decorator have similar structure diagrams since both rely on recursive composition to organize an open-ended number of objects.

A **Decorator** is like a Composite but only has one child component. There’s another significant difference: Decorator adds additional responsibilities to the wrapped object, while Composite just “sums up” its children’s results.

However, the patterns can also cooperate: you can use Decorator to extend the behavior of a specific object in the Composite tree.

Designs that make heavy use of Composite and Decorator can often benefit from using Prototype. Applying the pattern lets you clone complex structures instead of re-constructing them from scratch.

# Composite and Chain of Responsibility
Chain of Responsibility is often used in conjunction with Composite. In this case, when a leaf component gets a request, it may pass it through the chain of all of the parent components down to the root of the object tree.

# Composite and Visitor
Visitor can be used to execute an operation over an entire Composite tree.

# Composite and Iterator
You can use Iterators to traverse Composite trees.

# Composite and Flyweight
You can implement shared leaf nodes of the Composite tree as Flyweights to save some RAM.

# Decorator and Strategy
Decorator lets you change the skin of an object, while Strategy lets you change the guts.

# Decorator and Chain of Responsibility
They have very similar class structures. Both patterns rely on recursive composition to pass the execution through a series of objects. However, there are several crucial differences.

The CoR handlers can execute arbitrary operations independently of each other. They can also stop passing the request further at any point. On the other hand, various Decorators can extend the object’s behavior while keeping it consistent with the base interface. In addition, decorators aren’t allowed to break the flow of the request.

# Decorator and Strategy
Decorator lets you change the skin of an object, while Strategy lets you change the guts.


# State and Strategy
State can be considered as an extension of Strategy. Both patterns are based on composition: they change the behavior of the context by delegating some work to helper objects. Strategy makes these objects completely independent and unaware of each other. However, State doesn’t restrict dependencies between concrete states, letting them alter the state of the context at will.


# Memento and Command
You can use Command and Memento together when implementing “undo”. In this case, commands are responsible for performing various operations over a target object, while mementos save the state of that object just before a command gets executed.

# Memento and Iterator
You can use Command and Memento together when implementing “undo”. In this case, commands are responsible for performing various operations over a target object, while mementos save the state of that object just before a command gets executed.

# Memento and Prototype
Sometimes Prototype can be a simpler alternative to Memento. This works if the object, the state of which you want to store in the history, is fairly straightforward and doesn’t have links to external resources, or the links are easy to re-establish.

# Iterator and Visitor
You can use Visitor along with Iterator to traverse a complex data structure and execute some operation over its elements, even if they all have different classes.


# Command and Strategy
May look similar because you can use both to parameterize an object with some action. However, they have very different intents.

You can use Command to convert any operation into an object. The operation’s parameters become fields of that object. The conversion lets you defer execution of the operation, queue it, store the history of commands, send commands to remote services, etc.

On the other hand, Strategy usually describes different ways of doing the same thing, letting you swap these algorithms within a single context class.

# Command and Visitor
You can treat Visitor as a powerful version of the Command pattern. Its objects can execute operations over various objects of different classes.

# Observer and Mediator
The difference between Mediator and Observer is often elusive. In most cases, you can implement either of these patterns; but sometimes you can apply both simultaneously. Let’s see how we can do that.

The primary goal of Mediator is to eliminate mutual dependencies among a set of system components. Instead, these components become dependent on a single mediator object. The goal of Observer is to establish dynamic one-way connections between objects, where some objects act as subordinates of others.

There’s a popular implementation of the Mediator pattern that relies on Observer. The mediator object plays the role of publisher, and the components act as subscribers which subscribe to and unsubscribe from the mediator’s events. When Mediator is implemented this way, it may look very similar to Observer.

When you’re confused, remember that you can implement the Mediator pattern in other ways. For example, you can permanently link all the components to the same mediator object. This implementation won’t resemble Observer but will still be an instance of the Mediator pattern.

Now imagine a program where all components have become publishers, allowing dynamic connections between each other. There won’t be a centralized mediator object, only a distributed set of observers.


# Strategy and Template method
Template Method is based on inheritance: it lets you alter parts of an algorithm by extending those parts in subclasses. Strategy is based on composition: you can alter parts of the object’s behavior by supplying it with different strategies that correspond to that behavior. Template Method works at the class level, so it’s static. Strategy works on the object level, letting you switch behaviors at runtime.

# Strategy and State 
State can be considered as an extension of Strategy. Both patterns are based on composition: they change the behavior of the context by delegating some work to helper objects. Strategy makes these objects completely independent and unaware of each other. However, State doesn’t restrict dependencies between concrete states, letting them alter the state of the context at will.

# Strategy and Template Method
Template Method is based on inheritance: it lets you alter parts of an algorithm by extending those parts in subclasses. Strategy is based on composition: you can alter parts of the object’s behavior by supplying it with different strategies that correspond to that behavior. Template Method works at the class level, so it’s static. Strategy works on the object level, letting you switch behaviors at runtime.


# Visitor and Interpreter