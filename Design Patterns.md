## Design Patterns

- What Are Design Patterns?
- Creational Patterns
  - Singleton
  - Factory
- Structural Patterns
  - Adapter
  - Decorator
- Behavioral Patterns
  - Observer
  - Strategy
- Best Practices


## What Are Design Patterns?

Design patterns are common solutions to recurring problems in software design. They help improve code reusability, maintainability, and scalability.


## Creational Patterns

### Singleton

Ensures a class has only one instance.

```swift
class NetworkManager {
    static let shared = NetworkManager()
    private init() {}
}
```

### Factory

Creates objects without specifying the exact class.

```swift
protocol Shape {
    func draw()
}

class Circle: Shape {
    func draw() { print("Drawing Circle") }
}

class Square: Shape {
    func draw() { print("Drawing Square") }
}

class ShapeFactory {
    static func getShape(type: String) -> Shape {
        switch type {
        case "circle": return Circle()
        case "square": return Square()
        default: fatalError("Unknown shape")
        }
    }
}
```

---

## Structural Patterns

### Adapter

Allows incompatible interfaces to work together.

```swift
protocol OldPrinter {
    func oldPrint(text: String)
}

class ModernPrinter {
    func newPrint(text: String) {
        print("Printing: \(text)")
    }
}

class Adapter: OldPrinter {
    let printer = ModernPrinter()
    func oldPrint(text: String) {
        printer.newPrint(text: text)
    }
}
```

### Decorator

Adds behavior to an object dynamically.

```swift
protocol Coffee {
    func cost() -> Double
}

class SimpleCoffee: Coffee {
    func cost() -> Double { 5.0 }
}

class MilkDecorator: Coffee {
    let base: Coffee
    init(base: Coffee) { self.base = base }
    func cost() -> Double { base.cost() + 1.5 }
}
```

---

## Behavioral Patterns

### Observer

Allows objects to be notified of state changes.

```swift
class Publisher {
    var observers = [() -> Void]()
    func subscribe(_ observer: @escaping () -> Void) {
        observers.append(observer)
    }
    func notify() {
        observers.forEach { $0() }
    }
}
```

### Strategy

Allows selecting an algorithm at runtime.

```swift
protocol SortStrategy {
    func sort(_ array: [Int]) -> [Int]
}

class AscendingSort: SortStrategy {
    func sort(_ array: [Int]) -> [Int] { array.sorted() }
}

class DescendingSort: SortStrategy {
    func sort(_ array: [Int]) -> [Int] { array.sorted(by: >) }
}

class Sorter {
    var strategy: SortStrategy
    init(strategy: SortStrategy) {
        self.strategy = strategy
    }
    func sort(_ array: [Int]) -> [Int] {
        return strategy.sort(array)
    }
}
```

---

## Best Practices

- Use patterns only when they solve real problems.
- Avoid overengineering with unnecessary abstractions.
- Understand intent and consequences of each pattern.
