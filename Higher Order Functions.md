# Higher Order Functions in Swift

Swift offers a rich set of higher-order functions to manipulate collections and sequences. Here’s a comprehensive list with examples and index:

### \* Core Functions

* `map(_:)`
* `filter(_:)`
* `reduce(_:_:)`
* `reduce(into:_:)`
* `compactMap(_:)`
* `flatMap(_:)`
* `forEach(_:)`
* `sorted(by:)`
* `reversed()`
* `joined()`

### \* Search & Conditionals

* `contains(where:)`
* `allSatisfy(_:)`
* `first(where:)`
* `min(by:)`, `max(by:)`
* `prefix(while:)`
* `drop(while:)`

### \* Slicing

* `prefix(_:)`, `suffix(_:)`
* `dropFirst(_:)`, `dropLast(_:)`
* `split(separator:)`

### \* Grouping & Indexing

* `enumerated()`
* `partition(by:)`
* `Dictionary(grouping:by:)`
* `Dictionary(uniqueKeysWithValues:)`

### \* Utility

* `zip(_:_:)`
* `stride(from:to:by:)`
* `lazy`
* `indices.map`

### \* Swift 5.7+ Additions

* `chunks(ofCount:)`
* `windows(ofCount:)`
* `compactMapValues(_:)`
* `sequence(first:next:)`

---

###  Core Functions

#### `map(_:)`

```swift
let numbers = [1, 2, 3]
let squares = numbers.map { $0 * $0 } // [1, 4, 9]
```

#### `filter(_:)`

```swift
let evenNumbers = numbers.filter { $0 % 2 == 0 } // [2]
```

#### `reduce(_:_:)`

```swift
let sum = numbers.reduce(0, +) // 6
```

#### `reduce(into:_:)`

```swift
let names = ["Anna", "Alex"]
let mapped = names.reduce(into: [:]) { $0[$1] = $1.count }
```

#### `compactMap(_:)`

```swift
let values = ["1", "two", "3"]
let ints = values.compactMap { Int($0) } // [1, 3]
```

#### `flatMap(_:)`

```swift
let nested = [[1, 2], [3, 4]]
let flattened = nested.flatMap { $0 } // [1, 2, 3, 4]
```

#### `forEach(_:)`

```swift
numbers.forEach { print($0) }
```

#### `sorted(by:)`

```swift
let sorted = numbers.sorted { $0 > $1 } // [3, 2, 1]
```

#### `reversed()`

```swift
let reversed = numbers.reversed() // [3, 2, 1]
```

#### `joined()`

```swift
let strings = [["a", "b"], ["c"]]
let joined = strings.joined() // ["a", "b", "c"]
```

### Search & Conditionals

#### `contains(where:)`

```swift
let hasEven = numbers.contains { $0 % 2 == 0 } // true
```

#### `allSatisfy(_:)`

```swift
let allPositive = numbers.allSatisfy { $0 > 0 } // true
```

#### `first(where:)`

```swift
let firstEven = numbers.first { $0 % 2 == 0 } // 2
```

#### `min(by:)`, `max(by:)`

```swift
let minVal = numbers.min(by: <) // 1
let maxVal = numbers.max(by: <) // 3
```

#### `prefix(while:)`

```swift
let lessThanThree = numbers.prefix { $0 < 3 } // [1, 2]
```

#### `drop(while:)`

```swift
let dropped = numbers.drop { $0 < 3 } // [3]
```

### Slicing

#### `prefix(_:)`, `suffix(_:)`

```swift
let firstTwo = numbers.prefix(2) // [1, 2]
let lastTwo = numbers.suffix(2) // [2, 3]
```

#### `dropFirst(_:)`, `dropLast(_:)`

```swift
let dropFirst = numbers.dropFirst() // [2, 3]
let dropLast = numbers.dropLast() // [1, 2]
```

#### `split(separator:)`

```swift
let words = "one two three".split(separator: " ") // ["one", "two", "three"]
```

### Grouping & Indexing

#### `enumerated()`

```swift
for (index, value) in numbers.enumerated() {
    print("\(index): \(value)")
}
```

#### `partition(by:)`

```swift
var arr = [30, 40, 20, 10]
let index = arr.partition { $0 > 25 } // Index at partition point
```

#### `Dictionary(grouping:by:)`

```swift
let names = ["Anna", "Alex", "Brian", "Jack"]
let grouped = Dictionary(grouping: names) { $0.first! }
```

#### `Dictionary(uniqueKeysWithValues:)`

```swift
let pairs = [(1, "one"), (2, "two")]
let dict = Dictionary(uniqueKeysWithValues: pairs)
```

### Utility

#### `zip(_:_:)`

```swift
let letters = ["a", "b", "c"]
let zipped = Array(zip(numbers, letters))
```

#### `stride(from:to:by:)`

```swift
for i in stride(from: 0, to: 10, by: 2) {
    print(i)
}
```

#### `lazy`

```swift
let lazyFiltered = numbers.lazy.filter { $0 > 1 }.map { $0 * 2 }
```

#### `indices.map`

```swift
let list = [10, 20, 30]
let indexed = list.indices.map { (index: $0, value: list[$0]) }
```

### 🆕 Swift 5.7+ Additions

#### `chunks(ofCount:)`

```swift
let chunked = Array([1, 2, 3, 4, 5, 6].chunks(ofCount: 2))
```

#### `windows(ofCount:)`

```swift
let windowed = Array([1, 2, 3, 4].windows(ofCount: 2))
```

#### `compactMapValues(_:)`

```swift
let dict = ["a": "1", "b": "two"]
let intDict = dict.compactMapValues { Int($0) } // ["a": 1]
```

#### `sequence(first:next:)`

```swift
let fib = sequence(state: (0, 1)) { state in
    defer { state = (state.1, state.0 + state.1) }
    return state.0
}.prefix(5)
```
