# Clean Architecture

Clean Architecture is a software design philosophy that separates software solutions into layers with clear responsibilities. It encourages a decoupled system that is easier to maintain, test, and scale.

1. What is Clean Architecture?
2. Key Principles
3. Layers of Clean Architecture
4. iOS Implementation
5. Pros and Cons
6. Folder Structure Example
7. Best Practices

---

## 1. What is Clean Architecture?

Clean Architecture was proposed by Robert C. Martin (Uncle Bob). It divides the system into concentric layers, each having distinct roles. The inner layers are independent of the outer layers, enabling better testability and decoupling.

---

## 2. Key Principles

- **Dependency Rule**: Inner layers should never depend on outer layers.
- **Separation of Concerns**: Each layer has a single responsibility.
- **Testability**: Because dependencies are inverted, it's easy to test components in isolation.

---

## 3. Layers of Clean Architecture

```
Entities → Use Cases → Interface Adapters → Frameworks & Drivers
```

- **Entities**: Core business logic and data structures.
- **Use Cases**: Application-specific business rules.
- **Interface Adapters**: Convert data between layers (ViewModels, Presenters).
- **Frameworks & Drivers**: UI, Networking, Database, etc.

---

## 4. iOS Implementation

- **Entities**: Plain Swift models (not dependent on frameworks).
- **Use Cases**: Protocols and interactors encapsulating app logic.
- **Interface Adapters**: ViewModels, Presenters that adapt UI to business logic.
- **Frameworks**: UIKit, SwiftUI, Alamofire, CoreData, etc.

---

## 5. Pros and Cons

**Pros:**
- High testability
- Loose coupling
- Easy to refactor

**Cons:**
- Initial setup can be complex
- More boilerplate code

---

## 6. Folder Structure Example

```
MyApp/
├── Entities/
├── UseCases/
├── InterfaceAdapters/
│   ├── ViewModels/
│   └── Presenters/
├── Frameworks/
│   ├── UI/
│   └── Network/
└── App/
    └── AppDelegate.swift
```

---

## 7. Best Practices

- Use protocols to define boundaries.
- Inject dependencies using constructor or protocols.
- Keep ViewModels thin and focused.
- Avoid business logic in ViewControllers.

---

> Clean Architecture improves maintainability and scalability, especially for medium-to-large iOS apps.
