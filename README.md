# Detailed Guide to Programming Principles

## **1. Software Design Principles**

### **Clean Code At All Costs**
**Explanation:** Clean code is code that is easy to read, understand, and maintain. It prioritizes readability and simplicity over cleverness. Clean code helps developers debug and scale systems efficiently.

**Code Example:**
```python
# Clean code example:
def calculate_area(width, height):
    if width <= 0 or height <= 0:
        raise ValueError("Width and height must be positive numbers.")
    return width * height

# Bad code example:
def cal(w, h):
    return w * h
```

**Further Reading:**
- [Clean Code: A Handbook of Agile Software Craftsmanship](https://www.goodreads.com/book/show/3735293-clean-code)

---

### **Maximise Cohesion**
**Explanation:** Cohesion refers to how closely related the responsibilities of a single module/class are. High cohesion ensures that a module is focused on a single task, making it easier to understand and maintain.

**Code Example:**
```python
# High cohesion example:
class OrderProcessor:
    def validate_order(self, order):
        # Validation logic
        pass

    def process_payment(self, payment):
        # Payment logic
        pass

# Low cohesion example:
class OrderManager:
    def manage_order(self, order, payment):
        # Mixed responsibilities
        pass
```

**Further Reading:**
- [Cohesion in Object-Oriented Design](https://en.wikipedia.org/wiki/Cohesion_(computer_science))

---

### **Minimise Coupling**
**Explanation:** Coupling refers to the degree of dependency between modules. Low coupling ensures that changes in one module have minimal impact on others.

**Code Example:**
```python
# Low coupling example:
class PaymentGateway:
    def process_payment(self, payment):
        pass

class OrderProcessor:
    def __init__(self, payment_gateway):
        self.payment_gateway = payment_gateway

    def process_order(self, order):
        self.payment_gateway.process_payment(order.payment)

# High coupling example:
class OrderProcessor:
    def process_order(self, order):
        # Direct dependency on payment logic
        pass
```

**Further Reading:**
- [Coupling in Software Engineering](https://en.wikipedia.org/wiki/Coupling_(computer_programming))

---

### **Encapsulate What Changes**
**Explanation:** Isolate parts of the system that are likely to change to minimize the ripple effects of modifications.

**Code Example:**
```python
# Encapsulation example:
class Logger:
    def log(self, message):
        print(message)

class App:
    def __init__(self, logger):
        self.logger = logger

    def run(self):
        self.logger.log("Application started.")
```

**Further Reading:**
- [Encapsulation and Design Principles](https://refactoring.guru/design-patterns/principles)

---

### **Hide Implementation Details**
**Explanation:** Abstract the complexity of the implementation, exposing only what is necessary.

**Code Example:**
```python
# Hiding implementation details:
class DatabaseConnection:
    def __init__(self, connection_string):
        self._connection_string = connection_string

    def connect(self):
        return f"Connected to {self._connection_string}"

# Usage:
db = DatabaseConnection("localhost:5432")
print(db.connect())
```

**Further Reading:**
- [Abstraction in Programming](https://www.geeksforgeeks.org/abstraction-in-python/)

---

## **2. Object-Oriented Design (SOLID Principles)**

### **Single Responsibility Principle (SRP)**
**Explanation:** Each class should have only one reason to change, meaning it should have one responsibility.

**Code Example:**
```python
# Following SRP:
class User:
    def __init__(self, name):
        self.name = name

class UserRepository:
    def save_user(self, user):
        # Save logic
        pass
```

**Further Reading:**
- [SRP on Stack Overflow](https://stackoverflow.com/questions/47882/what-is-the-single-responsibility-principle)

---

### **Open/Closed Principle (OCP)**
**Explanation:** A class should be open for extension but closed for modification.

**Code Example:**
```python
# OCP example:
class Shape:
    def area(self):
        pass

class Rectangle(Shape):
    def area(self):
        return self.width * self.height

class Circle(Shape):
    def area(self):
        return 3.14 * self.radius ** 2
```

**Further Reading:**
- [OCP Explained](https://www.geeksforgeeks.org/open-closed-principle-in-java-with-examples/)

---

### **Liskov Substitution Principle (LSP)**
**Explanation:** Subtypes must be substitutable for their base types.

**Code Example:**
```python
# LSP example:
class Bird:
    def fly(self):
        pass

class Sparrow(Bird):
    def fly(self):
        print("Sparrow flying")

class Penguin(Bird):
    pass # Violates LSP as Penguin can't fly
```

**Further Reading:**
- [LSP on GeeksforGeeks](https://www.geeksforgeeks.org/liskov-substitution-principle-with-example/)

---

### **Interface Segregation Principle (ISP)**
**Explanation:** A class should not be forced to implement interfaces it does not use.

**Code Example:**
```python
# ISP example:
class Printer:
    def print(self):
        pass

class Scanner:
    def scan(self):
        pass

class AllInOnePrinter(Printer, Scanner):
    def print(self):
        print("Printing")

    def scan(self):
        print("Scanning")
```

**Further Reading:**
- [ISP Overview](https://www.geeksforgeeks.org/interface-segregation-principle/)

---

### **Dependency Inversion Principle (DIP)**
**Explanation:** High-level modules should not depend on low-level modules. Both should depend on abstractions.

**Code Example:**
```python
# DIP example:
class DatabaseInterface:
    def connect(self):
        pass

class MySQLDatabase(DatabaseInterface):
    def connect(self):
        print("Connecting to MySQL")

class Application:
    def __init__(self, db: DatabaseInterface):
        self.db = db

    def start(self):
        self.db.connect()

# Usage:
db = MySQLDatabase()
app = Application(db)
app.start()
```

**Further Reading:**
- [Dependency Inversion Principle on Refactoring Guru](https://refactoring.guru/design-patterns/principles)

---

## **3. Programming Paradigms & Practices**

### **Creation Over Legacy**
**Explanation:** Prefer creating new, clean implementations over maintaining outdated and complex legacy code.

**Code Example:**
```python
# Example of creation over legacy:
# Legacy code:
class LegacySystem:
    def perform_task(self):
        print("Performing task in a legacy way.")

# New implementation:
class ModernSystem:
    def perform_task(self):
        print("Performing task with modern approach.")

# Usage:
system = ModernSystem()
system.perform_task()
```

**Further Reading:**
- [Modernizing Legacy Systems](https://martinfowler.com/articles/microservices.html)

---

### **Command Query Separation (CQS)**
**Explanation:** A method should either perform an action (command) or return data (query), but not both.

**Code Example:**
```python
# CQS example:
class Account:
    def __init__(self):
        self.balance = 0

    def deposit(self, amount):
        self.balance += amount  # Command

    def get_balance(self):
        return self.balance  # Query
```

**Further Reading:**
- [CQS Principle](https://martinfowler.com/bliki/CommandQuerySeparation.html)

---
```markdown
### **4. Agile and Development Methodologies**

#### **Agile**

Agile is an iterative and incremental software development methodology that emphasizes flexibility, collaboration, and customer satisfaction. It encourages continuous delivery of small, functional software components, allowing for quicker adaptation to changes in requirements and ensuring higher-quality products.

- **Key Features**:
  - Iterative process
  - Flexibility in changes
  - Regular feedback from stakeholders
  - Collaborative teams

**Code Example (Agile approach in Python development):**

```python
# Scrum-based iterative sprint example (Pseudocode)
def sprint_backlog():
    # Define sprint backlog (a list of user stories)
    backlog = [
        {"task": "Develop feature A", "priority": 1},
        {"task": "Fix bug B", "priority": 2}
    ]
    return backlog

def sprint_review():
    # Review the progress
    print("Sprint Completed! Reviewing progress...")
    return True

# Example of agile sprint cycle
def agile_sprint():
    sprint = sprint_backlog()
    print(f"Sprint backlog: {sprint}")
    if sprint_review():
        print("Ready for the next iteration.")
```

**Learn More**:  
- [Agile Methodology Explained](https://www.agilealliance.org/agile101/) - A detailed explanation of Agile principles and practices.

#### **Scrum**

Scrum is a framework for Agile project management, specifically designed to promote collaboration, adaptability, and speed in software development. It organizes work into fixed-length iterations known as sprints, typically lasting 2-4 weeks, and includes roles such as Scrum Master, Product Owner, and Development Team.

- **Key Features**:
  - Sprint-based approach
  - Daily standups (Scrum meetings)
  - Regular reviews and retrospectives
  - Defined roles within the team

**Learn More**:  
- [Scrum Guide](https://www.scrum.org/resources/scrum-guide) - The official guide to Scrum framework and practices.

#### **Test-Driven Development (TDD)**

TDD is a software development process where you write tests before writing the actual code. The cycle of TDD consists of writing a test, writing just enough code to pass the test, and then refactoring the code to improve its structure.

- **Key Features**:
  - Write tests before code
  - Short development cycles
  - Helps to ensure high code quality
  - Refactor code after testing

**Code Example (Python TDD):**

```python
import unittest

# Example function to be tested
def add(a, b):
    return a + b

# Unit test case
class TestAddition(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(2, 3), 5)

if __name__ == '__main__':
    unittest.main()
```

**Learn More**:  
- [Test-Driven Development Overview](https://www.agilealliance.org/glossary/tdd/) - In-depth explanation of TDD and its practices.

#### **Domain-Driven Design (DDD)**

DDD is an approach to software development that emphasizes collaboration between developers and domain experts to create a shared understanding of the business problem and solution. The primary goal of DDD is to model complex software based on the domain's structure and language.

- **Key Features**:
  - Focus on the core domain
  - Ubiquitous language between developers and domain experts
  - Bounded contexts and aggregates

**Learn More**:  
- [Domain-Driven Design Explained](https://martinfowler.com/tags/domain%20driven%20design.html) - A collection of resources on Domain-Driven Design.

---

### **5. Testing Principles**

#### **FIRST Principles of Testing**

The FIRST principles are a set of guidelines for writing effective and efficient tests. The acronym stands for:

- **Fast**: Tests should run quickly.
- **Independent**: Tests should be independent and not rely on each other.
- **Repeatable**: Tests should produce the same results each time.
- **Self-validating**: Tests should clearly show whether they pass or fail.
- **Timely**: Tests should be written at the appropriate time in the development process.

**Learn More**:  
- [FIRST Principles of Testing](https://www.agiletester.co.uk/first-principles-testing/) - A detailed explanation of the FIRST principles.

#### **Arrange, Act, Assert (AAA)**

AAA is a pattern for writing clear and concise tests. It divides a test into three parts:

- **Arrange**: Set up the initial conditions.
- **Act**: Execute the code being tested.
- **Assert**: Verify that the expected outcome has been achieved.

**Code Example (Python Test with AAA):**

```python
import unittest

def subtract(a, b):
    return a - b

class TestSubtraction(unittest.TestCase):
    def test_subtract(self):
        # Arrange
        a, b = 10, 5
        expected = 5
        
        # Act
        result = subtract(a, b)
        
        # Assert
        self.assertEqual(result, expected)

if __name__ == '__main__':
    unittest.main()
```

**Learn More**:  
- [Arrange-Act-Assert Pattern](https://martinfowler.com/bliki/ArrangeActAssert.html) - Explanation of the AAA pattern for writing tests.

---

### **6. Database Design**

#### **ACID in DB**

ACID stands for Atomicity, Consistency, Isolation, and Durability, which are the four properties that ensure reliable transactions in a database:

- **Atomicity**: Ensures that all operations within a transaction are completed successfully or none at all.
- **Consistency**: Ensures that a transaction brings the database from one valid state to another.
- **Isolation**: Ensures that concurrent transactions do not affect each other.
- **Durability**: Ensures that once a transaction is committed, it will persist even in the case of system failures.

**Learn More**:  
- [ACID Properties in Database](https://www.geeksforgeeks.org/acid-properties-in-dbms/) - A detailed breakdown of the ACID properties.

#### **Full, Right, Inner, and Left Join**

SQL joins are used to combine records from two or more tables based on related columns. Here are the main types of joins:

- **Inner Join**: Returns records that have matching values in both tables.
- **Left Join**: Returns all records from the left table, and matching records from the right table.
- **Right Join**: Returns all records from the right table, and matching records from the left table.
- **Full Join**: Returns records when there is a match in either table.

**Code Example (SQL Join Queries):**

```sql
-- Inner Join
SELECT employees.name, departments.name
FROM employees
INNER JOIN departments ON employees.department_id = departments.id;

-- Left Join
SELECT employees.name, departments.name
FROM employees
LEFT JOIN departments ON employees.department_id = departments.id;

-- Right Join
SELECT employees.name, departments.name
FROM employees
RIGHT JOIN departments ON employees.department_id = departments.id;

-- Full Join
SELECT employees.name, departments.name
FROM employees
FULL JOIN departments ON employees.department_id = departments.id;
```

**Learn More**:  
- [SQL Joins Explained](https://www.w3schools.com/sql/sql_join.asp) - An in-depth guide to SQL joins with examples.

### **7. Architectural Patterns**

Architectural patterns define how software components are organized and interact within a system. They provide a blueprint for the structure of a program, facilitating maintainability, scalability, and separation of concerns. Below are some commonly used architectural patterns:

#### **MVC (Model-View-Controller)**  
The **MVC** pattern separates an application into three main components:

1. **Model**: Represents the data and the business logic of the application.
2. **View**: Represents the UI and presentation logic.
3. **Controller**: Acts as an intermediary between the Model and the View, handling user inputs and updating the View.

**Example in Code:**

```python
# Model: Handles the data
class User:
    def __init__(self, name, email):
        self.name = name
        self.email = email

# View: Displays the data
class UserView:
    def show_user(self, user):
        print(f"Name: {user.name}, Email: {user.email}")

# Controller: Connects the model and view
class UserController:
    def __init__(self, user, view):
        self.user = user
        self.view = view

    def update_view(self):
        self.view.show_user(self.user)
        
# Usage
user = User('Alice', 'alice@example.com')
view = UserView()
controller = UserController(user, view)
controller.update_view()
```

**Further Reading:**
You can learn more about MVC in detail on the [MVC Design Pattern - Tutorial](https://www.tutorialspoint.com/design_pattern/mvc_pattern.htm).

#### **MVT (Model-View-Template)**  
In contrast to MVC, the **MVT** pattern is used by Django. It has three components:

1. **Model**: Defines the structure of the data and the database.
2. **View**: A user-facing component that processes HTTP requests and returns HTTP responses. Unlike MVC, the "view" in MVT is about handling logic.
3. **Template**: The frontend HTML structure, where the dynamic content is displayed.

**Example in Code (Django):**

```python
# Model (Django Model)
from django.db import models

class User(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()

# Template (HTML Template)
# user_detail.html
# <h1>{{ user.name }}</h1>
# <p>{{ user.email }}</p>

# View (Django View)
from django.shortcuts import render
from .models import User

def user_detail(request, user_id):
    user = User.objects.get(id=user_id)
    return render(request, 'user_detail.html', {'user': user})
```

**Further Reading:**
Learn more about MVT and how it works in Django from the [Django Documentation](https://docs.djangoproject.com/en/stable/misc/design-philosophies/).

#### **Separation of Concerns (SoC)**  
Separation of Concerns is a design principle that advocates for dividing a software system into distinct sections, where each section is responsible for a specific task. This helps in reducing complexity and increasing maintainability.

**Example in Code:**
```python
# Different concerns separated into different classes
class Database:
    def connect(self):
        print("Connected to the database")

class UI:
    def display(self):
        print("Displaying UI")

class BusinessLogic:
    def process_data(self, data):
        print(f"Processing {data}")
```

**Further Reading:**
You can read more about Separation of Concerns in software engineering on [Wikipedia](https://en.wikipedia.org/wiki/Separation_of_concerns).

---

### **8. Other Fundamental Concepts**

These concepts are key to writing clean, maintainable, and efficient code.

#### **DRY (Don’t Repeat Yourself)**  
The DRY principle emphasizes the importance of avoiding redundancy in code. If you find that code is repeated, it should be refactored into a function, class, or module to make it reusable.

**Example in Code:**
```python
# Violating DRY
def calculate_area(length, width):
    return length * width

def calculate_perimeter(length, width):
    return 2 * (length + width)

# Following DRY
def calculate_area(length, width):
    return length * width

def calculate_perimeter(length, width):
    return 2 * (length + width)

def calculate_area_and_perimeter(length, width):
    area = calculate_area(length, width)
    perimeter = calculate_perimeter(length, width)
    return area, perimeter
```

**Further Reading:**
Find out more about the DRY principle on [Wikipedia](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself).

#### **KISS (Keep It Simple, Stupid)**  
The KISS principle advocates for simplicity in software design. It suggests that the simplest solution is usually the best one and that unnecessary complexity should be avoided.

**Example in Code:**
```python
# Complex solution
def get_grade(score):
    if score > 90:
        return 'A'
    elif score > 80:
        return 'B'
    elif score > 70:
        return 'C'
    elif score > 60:
        return 'D'
    else:
        return 'F'

# Simple solution (KISS)
def get_grade(score):
    return 'A' if score > 90 else 'F'
```

**Further Reading:**
Read more about the KISS principle on [Wikipedia](https://en.wikipedia.org/wiki/KISS_principle).

#### **Connascence**  
Connascence refers to the degree of dependency between different modules or components. A low degree of connascence is preferable, as it suggests that modules are less interdependent and easier to modify independently.

**Example in Code:**
```python
# High connascence: tight coupling between components
class User:
    def __init__(self, name, email):
        self.name = name
        self.email = email

    def send_email(self, message):
        print(f"Sending email to {self.email}: {message}")

# Low connascence: decoupled components
class EmailService:
    def send_email(self, email, message):
        print(f"Sending email to {email}: {message}")

class User:
    def __init__(self, name, email):
        self.name = name
        self.email = email

user = User('Alice', 'alice@example.com')
email_service = EmailService()
email_service.send_email(user.email, "Welcome!")
```

**Further Reading:**
Learn more about Connascence from the [Wikipedia article on Connascence](https://en.wikipedia.org/wiki/Connascence).

---

### **9. Comprehensive Principles**

These principles guide the structure and maintainability of large systems.

#### **SOLID Principles**  
The **SOLID** principles are a set of object-oriented design principles that promote maintainability and scalability. They are:

1. **SRP (Single Responsibility Principle)**: A class should have only one reason to change.
2. **OCP (Open/Closed Principle)**: Software entities should be open for extension but closed for modification.
3. **LSP (Liskov Substitution Principle)**: Subtypes must be substitutable for their base types.
4. **ISP (Interface Segregation Principle)**: Clients should not be forced to depend on interfaces they do not use.
5. **DIP (Dependency Inversion Principle)**: High-level modules should not depend on low-level modules; both should depend on abstractions.

**Example in Code (SRP):**
```python
# Violating SRP: A class with multiple responsibilities
class Employee:
    def calculate_salary(self):
        pass
    
    def save_employee(self):
        pass

# Following SRP: Separate classes for different responsibilities
class SalaryCalculator:
    def calculate_salary(self, employee):
        pass

class EmployeeDatabase:
    def save_employee(self, employee):
        pass
```

**Further Reading:**
Learn more about SOLID principles on [Wikipedia](https://en.wikipedia.org/wiki/SOLID).

#### **Creation Over Legacy**  
This principle encourages the creation of new systems and frameworks instead of extending or modifying old, legacy systems. It helps in avoiding limitations imposed by outdated technologies.

**Further Reading:**
For more on this topic, you can read [Why New Is Better Than Old](https://www.freecodecamp.org/news/why-new-architecture-over-legacy/).

#### **Yangi**  
The **Yangi** principle is a lesser-known concept that emphasizes the importance of evolving practices in software development. It promotes continuous improvement and adaptation of new technologies.

**Further Reading:**
Learn more about emerging software principles like Yangi at [Yangi: Principles of Software Evolution](https://medium.com).

---
