# Swift Language Fundamentals

Swift is a powerful and intuitive programming language created by Apple for building apps on iOS, macOS, watchOS, and tvOS. It’s designed to be safe, fast, and expressive.

---


* Optionals

  * Nil-Coalescing Operator
  * Optional Chaining
  * Optional Binding
  * `guard` Statement
  * `defer` Statement
* Lazy Keyword
* `[weak self]` & `[unowned self]`
* Enums
* Class vs Struct
* Closures

  * `@escaping` & `@nonescaping`
* Protocols & Delegates

---

## Optionals

```swift
var name: String? = "John"
```

### Nil-Coalescing Operator (`??`)

```swift
let displayName = name ?? "Guest"
```

### Optional Chaining

```swift
let city = person?.address?.city
```

### Optional Binding

```swift
if let name = name {
    print(name)
}
```

### `guard` Statement

```swift
guard let name = name else { return }
```

### `defer` Statement

```swift
func test() {
    defer { print("done") }
    print("start")
}
```

---

## Lazy Keyword

```swift
lazy var name: String = computeName()
```

---

## `[weak self]` & `[unowned self]`

```swift
someClosure = { [weak self] in
    self?.doSomething()
}
```

---

## Enums

```swift
enum Direction {
    case north, south, east, west
}
```

---

## Class vs Struct

```swift
class A {}
struct B {}
```

---

## Closures

```swift
let greet = { (name: String) in
    print("Hello, \(name)")
}
```

### `@escaping` & `@nonescaping`

```swift
func fetchData(completion: @escaping () -> Void) {}
```

---

## Protocols & Delegates

```swift
protocol MyDelegate: AnyObject {
    func didUpdate()
}
```

class MyClass {
weak var delegate: MyDelegate?

```
func update() {
    delegate?.didUpdate()
}
```
