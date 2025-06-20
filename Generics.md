# Generics

* What are Generics?
* Basic Generic Function
* Generic Types (Structs, Classes, Enums)
* Generic Constraints
* Associated Types in Protocols
* Advanced: Generic Protocol Extensions
* Advanced: Type Erasure with Generics
* Benefits


## 1. What are Generics?

Generics allow you to write flexible and reusable functions, types, and data structures that can work with any type.

Instead of duplicating code for different data types (e.g. Int, String), you can write generic code that works across all types.

---

## 2. Basic Generic Function

```swift
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
    let temp = a
    a = b
    b = temp
}

var x = 10
var y = 20
swapTwoValues(&x, &y) // x = 20, y = 10

var first = "Apple"
var second = "Banana"
swapTwoValues(&first, &second) // first = "Banana"
```

---

## 3. Generic Types (Structs, Classes, Enums)

```swift
struct Stack<Element> {
    var items: [Element] = []

    mutating func push(_ item: Element) {
        items.append(item)
    }

    mutating func pop() -> Element? {
        return items.popLast()
    }
}

var intStack = Stack<Int>()
intStack.push(1)
intStack.push(2)
intStack.pop() // 2

var stringStack = Stack<String>()
stringStack.push("Swift")
stringStack.push("Generics")
```

---

## 4. Generic Constraints

You can add constraints to specify that a type must conform to a certain protocol.

```swift
func findIndex<T: Equatable>(of value: T, in array: [T]) -> Int? {
    for (index, element) in array.enumerated() {
        if element == value {
            return index
        }
    }
    return nil
}

findIndex(of: 3, in: [1, 2, 3, 4]) // 2
```

---

## 5. Associated Types in Protocols

```swift
protocol Container {
    associatedtype Item
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }
}

struct IntContainer: Container {
    var items: [Int] = []

    mutating func append(_ item: Int) {
        items.append(item)
    }

    var count: Int {
        return items.count
    }

    subscript(i: Int) -> Int {
        return items[i]
    }
}
```

---

## 6. Advanced: Generic Protocol Extensions

You can extend a generic protocol with constraints:

```swift
extension Container where Item: Equatable {
    func contains(_ item: Item) -> Bool {
        for i in 0..<count {
            if self[i] == item {
                return true
            }
        }
        return false
    }
}
```

---

## 7. Advanced: Type Erasure with Generics

Use type erasure when you want to hide the generic type from outside consumers.

```swift
protocol AnyPrintable {
    func printValue()
}

struct PrintableBox<T>: AnyPrintable {
    var value: T
    func printValue() {
        print(value)
    }
}

let items: [AnyPrintable] = [
    PrintableBox(value: "Hello"),
    PrintableBox(value: 42),
    PrintableBox(value: true)
]

items.forEach { $0.printValue() }
```

---

## 8. Benefits

* Avoid code duplication
* More readable and maintainable
* Type-safe and flexible

Let me know if you’d like to add **Generic Typealiases**, **Recursive Generics**, or a **Real-World Architecture Example**!
