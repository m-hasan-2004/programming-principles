# Design Patterns Overview
What Are Design Patterns?

Design patterns are reusable solutions to common problems in software design. They represent best practices refined through experience by developers. These patterns help simplify complex design issues by providing templates that can be customized to solve specific challenges. Design patterns are categorized into three main types:

Creational Patterns: Focus on object creation mechanisms, ensuring that objects are created in a way suitable for the situation.

Structural Patterns: Deal with the composition of classes or objects, ensuring that the relationships between entities are efficient and flexible.

Behavioral Patterns: Concerned with communication between objects, facilitating responsibility and interaction.

Understanding and applying design patterns not only improve code reusability and readability but also reduce development time. They are not rigid solutions but adaptable guidelines for problem-solving in programming.

---

## Creational Design Patterns

### Singleton
The Singleton design pattern ensures that a class has only one instance and provides a global point of access to it. 

**Use Case:** Useful in cases like database connections or configuration management.

**Example:**
```python
class Singleton:
    _instance = None

    def __new__(cls, *args, **kwargs):
        if not cls._instance:
            cls._instance = super(Singleton, cls).__new__(cls, *args, **kwargs)
        return cls._instance
```

**Further Reading:** [Singleton Pattern](https://refactoring.guru/design-patterns/singleton)

### Prototype
The Prototype pattern is used to create duplicate objects while keeping performance in mind. 

**Use Case:** When creating complex objects where copying is more efficient than building from scratch.

**Example:**
```python
import copy

class Prototype:
    def __init__(self):
        self._objects = {}

    def register(self, name, obj):
        self._objects[name] = obj

    def clone(self, name):
        return copy.deepcopy(self._objects.get(name))
```

**Further Reading:** [Prototype Pattern](https://refactoring.guru/design-patterns/prototype)

### Builder
The Builder pattern separates the construction of a complex object from its representation, allowing the same construction process to create different representations.

**Use Case:** When dealing with complex object creation that involves several steps.

**Example:**
```python
class Builder:
    def __init__(self):
        self.product = Product()

    def build_part(self, part):
        self.product.parts.append(part)

class Product:
    def __init__(self):
        self.parts = []
```

**Further Reading:** [Builder Pattern](https://refactoring.guru/design-patterns/builder)

### Factory
The Factory pattern provides an interface for creating objects but allows subclasses to alter the type of objects created.

**Use Case:** When the object creation logic is complex or varies based on input parameters.

**Example:**
```python
class Factory:
    def create_object(self, obj_type):
        if obj_type == 'type1':
            return ObjectType1()
        elif obj_type == 'type2':
            return ObjectType2()
```

**Further Reading:** [Factory Pattern](https://refactoring.guru/design-patterns/factory-method)

---

## Structural Design Patterns

### Facade
The Facade pattern provides a simplified interface to a larger body of code.

**Use Case:** To provide a unified interface to a complex system.

**Example:**
```python
class Facade:
    def operation(self):
        subsystem1 = SubSystem1()
        subsystem2 = SubSystem2()
        return subsystem1.action() + subsystem2.action()
```

**Further Reading:** [Facade Pattern](https://refactoring.guru/design-patterns/facade)

### Proxy
The Proxy pattern acts as a surrogate or placeholder for another object to control access to it.

**Use Case:** Managing access, caching, or logging for an object.

**Example:**
```python
class Proxy:
    def __init__(self, real_subject):
        self._real_subject = real_subject

    def request(self):
        return self._real_subject.request()
```

**Further Reading:** [Proxy Pattern](https://refactoring.guru/design-patterns/proxy)

---

## Behavioral Design Patterns

### Iterator
The Iterator pattern provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.

**Use Case:** Traversing collections such as lists or arrays.

**Example:**
```python
class Iterator:
    def __init__(self, collection):
        self.collection = collection
        self.index = 0

    def next(self):
        if self.index < len(self.collection):
            value = self.collection[self.index]
            self.index += 1
            return value
        raise StopIteration
```

**Further Reading:** [Iterator Pattern](https://refactoring.guru/design-patterns/iterator)

### Observer
The Observer pattern defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified.

**Use Case:** Event handling systems.

**Example:**
```python
class Subject:
    def __init__(self):
        self._observers = []

    def add_observer(self, observer):
        self._observers.append(observer)

    def notify_observers(self):
        for observer in self._observers:
            observer.update()
```

**Further Reading:** [Observer Pattern](https://refactoring.guru/design-patterns/observer)

### Mediator
The Mediator pattern reduces coupling between classes by introducing a mediator object that handles communication between them.

**Use Case:** Managing complex object interactions.

**Example:**
```python
class Mediator:
    def __init__(self):
        self._components = []

    def register(self, component):
        self._components.append(component)

    def mediate(self, sender, event):
        for component in self._components:
            if component != sender:
                component.receive(event)
```

**Further Reading:** [Mediator Pattern](https://refactoring.guru/design-patterns/mediator)

### State
The State pattern allows an object to alter its behavior when its internal state changes.

**Use Case:** Managing object behavior based on state.

**Example:**
```python
class State:
    def handle(self):
        pass

class Context:
    def __init__(self, state):
        self.state = state

    def request(self):
        self.state.handle()
```

**Further Reading:** [State Pattern](https://refactoring.guru/design-patterns/state)

---

## How to Use Design Patterns

1. **Understand the Problem:** Clearly define the problem you're trying to solve.
2. **Choose the Right Pattern:** Select a pattern that aligns with your requirements.
3. **Implement and Refactor:** Apply the pattern incrementally and refactor as needed.
4. **Test Extensively:** Ensure the pattern works as intended and doesn't introduce unnecessary complexity.

---

## Using Design Patterns in Django Projects

### Creational Patterns in Django
- **Singleton:** Used in settings or configurations to ensure a single instance.
- **Factory:** Applied in Django forms or serializers to dynamically create instances.

### Structural Patterns in Django
- **Facade:** Simplifies interaction with complex views or APIs.
- **Proxy:** Used in ORM for database interactions and query optimization.

### Behavioral Patterns in Django
- **Observer:** Implemented in Django signals to handle event-driven programming.
- **State:** Utilized in workflows like order processing or user state management.

**Example:**
```python
# Observer with Django signals
from django.db.models.signals import post_save
from django.dispatch import receiver
from .models import UserProfile

@receiver(post_save, sender=User)
def create_user_profile(sender, instance, created, **kwargs):
    if created:
        UserProfile.objects.create(user=instance)
```

By leveraging these patterns effectively, Django developers can build scalable and maintainable applications tailored to specific project needs.

