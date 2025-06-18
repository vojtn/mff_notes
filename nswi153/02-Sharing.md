[Back to overview](/Readme.md)

# Design patterns

## Front Controller

- A **single entry point** for handling all requests (commonly seen in web frameworks).
- Manages:
  - **Routing**: Determines which controller/action to invoke.
  - **Dispatching**: Calls appropriate handlers or controllers.
- Centralizes request handling logic for better control and consistency.

---

## Dependency Injection (DI)

- A design pattern where **components receive their dependencies from the outside** rather than creating them internally.
- Promotes:
  - **Loose coupling**
  - **Improved testability**
  - **Inversion of control (IoC)**

### Notes:
- Unlike using constructors or service locators, DI allows more flexibility.
- Cyclic dependencies can arise and must be carefully managed.

---

## MVC (Model View Controller)
- A widely-used pattern for separating application logic.
- Originally designed for **Smalltalk** (1980s).

### Components:
- **Model** – Manages data and business rules.
- **View** – UI representation of the data (can have multiple views).
- **Controller** – Handles user input and updates model/view accordingly.

No strict standard for MVC — implementations vary widely.

![](/img/MVC.png)
--- 

## MVP
- Variation of MVC that **separates the View and Model more explicitly**.

### Components:
- **Model** – Business logic and data.
- **View** – Passive UI component (dumb).
- **Presenter** – Handles all logic and **acts as an intermediary**.

Presenter often stores **state** and pushes updates to the view.

![](/img/MVP.png)
---

## MVVM (Model-View-ViewModel)
- Popular in modern frontend frameworks and web development like Angular or Vue.js
- Based on **data binding and reactivity**:
  - The **ViewModel** connects the View and the Model.
  - Any change in the ViewModel automatically reflects in the View and vice versa.
- Reduces manual DOM manipulation or UI updates.

### Components:
- **Model** – App data and business logic.
- **View** – UI.
- **ViewModel** – Exposes data and logic to the View with binding.

### Advantages:
- **Two-way binding** keeps UI and state in sync.
- **Reduces boilerplate** and manual DOM updates.

![](/img/MVVM.png)

---

## MVVMC (Model-View-ViewModel-Coordinator)

- Extension of **MVVM**, introducing the **Coordinator** pattern.
- **Coordinator** is responsible for:
  - Handling navigation flow between screens (triplets).
  - Decoupling navigation logic from ViewModels and Views.
- Improves **separation of concerns**:
  - **Model**: Business logic and data.
  - **View**: UI.
  - **ViewModel**: UI-related logic and data-binding.
  - **Coordinator**: Navigation and flow management.
- Common in complex iOS apps (Swift).

![](/img/MVVMC.png)
---

## VIPER

- Clean architecture pattern often used in **iOS development**.
- Stands for:
  - **View**: Displays information and receives user input.
  - **Interactor**: Contains business logic (formerly “Model”).
  - **Presenter**: Formats data from Interactor to display.
  - **Entity**: Basic data model objects.
  - **Router**: Handles navigation (like a Coordinator).
- **Advantages**:
  - High modularity and testability.
  - Clear separation of responsibilities.
  - Supports large, complex codebases.
- **Drawbacks**:
  - High initial complexity and boilerplate.
  - May be overkill for small projects.

![](/img/VIPER.png)

---

## MVT (Model-View-Template)

- Architectural pattern popularized by **Django (Python web framework)**.
- Very similar to MVC but with different naming:
  - **Model**: Data and business logic.
  - **View**: Processes requests, fetches data, and passes it to the template.
  - **Template**: Handles presentation (HTML).
- Key distinction:
  - Django’s "View" = Controller (in MVC)
  - Django’s "Template" = View (in MVC)
- **Goal**: Cleanly separate concerns of:
  - **What data is presented** (Model/View)
  - **How it is presented** (Template)

 "Separate *what* the user sees from *how* they see it."

![](/img/MVT.png)

---

# Database
Data is often the **most critical part** of a system — many systems are designed around how data is stored, queried, and updated.

### ACID Properties
ACID ensures **reliability** of database transactions:
- Atomicity – transactions are all-or-nothing.
- Consistency – data remains valid and consistent before and after transactions.
- Isolation – concurrent transactions don’t interfere with each other.
- Durability – committed transactions persist even after failures.

### Procedures, Functions & Triggers
- **Stored Procedures/Functions** – reusable SQL code that runs on the database server.
- **Triggers** – automatically executed procedures in response to events (e.g., insert, update, delete).

---

## Data models

Defines the **structure and meaning** of data in a system.

### Key Concepts:
- **Model / Entity** – represents a real-world concept (e.g., User, Product).
- **Business Rules** – constraints and logic applied to the data (e.g., email must be unique).
- **Natural Definition** – model matches domain understanding.
- **Encapsulation** – abstract away internal data structure.
- **Object Relationships** – e.g., one-to-many, many-to-many between entities.

---

### ORM (Object-Relational-Mapping)

Technique that provides an **object-oriented interface** to a **relational database**.

### Pros:
- Avoids writing raw SQL.
- Maps tables to classes and rows to objects.
- Easier for developers familiar with object-oriented languages.

### Example:
- **Doctrine** (PHP)
- **Hibernate** (Java)
- **Entity Framework** (.NET)
- **SQLAlchemy** (Python)

---

## Dependency/package managers
Tools that manage **external libraries and modules** your project depends on.

### Examples:
- **vcpkg** – C/C++ package manager.
- **Maven** – Java dependency and build manager.
- **Composer** – PHP dependency manager.
- **npm / yarn** – Node.js/JavaScript.
- **pip** – Python.

---

### Dependency monitoring 

**How do we detect vulnerabilities in dependencies?**

- Tools analyze known vulnerabilities in libraries and their versions.
- Common services:
  - **Snyk**
  - **Dependabot (GitHub)**
  - **npm audit**
  - **OWASP Dependency-Check**
- Goal: Prevent deploying code with known security flaws.

## Linter

A **static code analysis tool** that checks your code for errors, potential bugs, or style violations.

- Helps enforce **coding standards**.
- Often integrated with IDEs.
- Language-specific examples:
  - **ESLint** – JavaScript/TypeScript
  - **Pylint** – Python
  - **Rubocop** – Ruby

## Prettier

A **code formatter** that ensures a consistent style across your codebase.

- Automatically formats code (e.g., spacing, indentation, quotes).
- Language support includes JavaScript, TypeScript, HTML, CSS, Markdown, and more.
- Not a linter – focuses on **style, not correctness**.
- Often used together with linters for a full code quality workflow.

---
[Back to overview](/Readme.md)
