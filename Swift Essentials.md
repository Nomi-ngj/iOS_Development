## Swift Essentials

* Properties
* Control Flow (if, for, while, switch)
* Collections (Array, Set, Dictionary)
* Keywords (let, var, in, is, as, defer, guard)
* Functions and Parameters
* Higher Order Functions
* Access Control
* Type Casting

## Properties

```swift
struct User {
    var name: String
    let id: Int
}

var user = User(name: "Nouman", id: 1)
user.name = "Ali" // 'id' can't be changed since it's a constant
```

---

## Control Flow

```swift
let score = 85
if score >= 90 {
    print("Excellent")
} else if score >= 80 {
    print("Good")
} else {
    print("Try again")
}

for i in 1...3 {
    print(i)
}

var count = 0
while count < 3 {
    print(count)
    count += 1
}

switch score {
case 90...100:
    print("A grade")
case 80..<90:
    print("B grade")
default:
    print("C grade")
}
```

---

## Collections

```swift
let array = ["iOS", "Swift"]
let set: Set = [1, 2, 3, 1] // Unique values only
var dictionary = ["name": "Nouman", "language": "Swift"]
```

---

## Keywords

```swift
let constant = 10
var variable = 20

for item in array {
    print(item)
}

if let casted = variable as? Int {
    print(casted)
}

guard let name = dictionary["name"] else { return }
defer { print("Always runs at the end of scope") }
```

---

## Functions and Parameters

```swift
func greet(name: String) -> String {
    return "Hello, \(name)!"
}

let message = greet(name: "Nouman")
```

---

## Higher Order Functions

```swift
let numbers = [1, 2, 3, 4]

let squared = numbers.map { $0 * $0 }
let even = numbers.filter { $0 % 2 == 0 }
let sum = numbers.reduce(0, +)
```

---

## Access Control

```swift
public class MyClass {
    private var secret = "hidden"
    internal var visible = true
    public var name = "Nouman"
}
```

---

## Type Casting

```swift
class Animal {}
class Dog: Animal {}

let pet: Animal = Dog()
if let dog = pet as? Dog {
    print("It’s a dog!")
}
```
