
## Memory Management in Swift

* What is Memory Management?
* Automatic Reference Counting (ARC)
* Strong References
* Retain Cycles
* Weak and Unowned References
* Closures and Capture Lists
* Memory Debugging
* Combine and Retain Cycles
* Swift Concurrency (async/await)
* Best Practices

---

## 1. What is Memory Management?

Memory management ensures that your app uses system memory efficiently, preventing leaks and crashes. Swift uses Automatic Reference Counting (ARC) to handle this behind the scenes.

---

## 2. Automatic Reference Counting (ARC)

ARC tracks how many strong references exist to a class instance. When that count hits zero, the instance is deallocated.

```swift
class Person {
    let name: String
    init(name: String) { self.name = name }
    deinit { print("\(name) is deallocated") }
}

var person: Person? = Person(name: "Nouman")
person = nil // ARC deallocates the instance
```

---

## 3. Strong References

By default, all references are strong. This means the object will not be deallocated as long as a strong reference exists.

```swift
class A {
    var b: B?
}

class B {
    var a: A?
}
```

---

## 4. Retain Cycles

When two instances hold strong references to each other, they create a retain cycle, preventing ARC from deallocating them.

```swift
class A {
    var b: B?
}

class B {
    var a: A?
}
```

---

## 5. Weak and Unowned References

To break retain cycles, use `weak` or `unowned` references.

- `weak`: Used when reference can become nil.
- `unowned`: Used when reference must always point to a valid instance.

```swift
class A {
    var b: B?
}

class B {
    weak var a: A?
}
```

```swift
class A {
    var b: B?
}

class B {
    unowned var a: A
    init(a: A) { self.a = a }
}
```

---

## 6. Closures and Capture Lists

Closures capture variables strongly by default, which can also cause retain cycles.

```swift
class MyClass {
    var name = "Swift"
    lazy var greet: () -> Void = { [weak self] in
        print("Hello, \(self?.name ?? "Unknown")")
    }
}
```

---

## 7. Memory Debugging

Use Xcode's tools to find memory leaks:

- **Debug Memory Graph**
- **Instruments (Leaks, Allocations)**

---

## 8. Combine and Retain Cycles

Combine publishers retain subscribers unless `[weak self]` is used.

```swift
cancellable = publisher
    .sink { [weak self] value in
        self?.doSomething(value)
    }
```

---

## 9. Swift Concurrency (async/await)

Actors and tasks can also create references that need to be handled carefully.

```swift
Task { [weak self] in
    await self?.fetchData()
}
```

---

## 10. Best Practices

- Prefer `weak` over `unowned` unless you're sure the instance will not be nil.
- Use `[weak self]` in closures and Combine subscriptions.
- Avoid deep object graphs with strong references everywhere.
- Profile your app with Instruments.
