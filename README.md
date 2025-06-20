# iOS Development Concepts

## [Swift Essential](https://github.com/Nomi-ngj/iOS_Development/blob/main/Swift%20Essentials.md)

* Properties
* Control Flow (`if`, `for`, `while`, `switch`)
* Collections (`Array`, `Set`, `Dictionary`)
* Keywords (`let`, `var`, `in`, `is`, `as`, `defer`, `guard`)
* Functions and Parameters
* Higher Order Functions
* Access Control
* Type Casting

## [Swift Language Fundamentals](https://github.com/Nomi-ngj/iOS_Development/blob/main/Swift%20Fundamental.md)

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

## [OOP Concepts](https://github.com/Nomi-ngj/iOS_Development/blob/main/OOP%20Concepts.md)
  * Inheritance
  * Polymorphism
  * Encapsulation
  * Abstraction

## [Higher Order Functions in Swift](https://github.com/Nomi-ngj/iOS_Development/blob/main/Higher%20Order%20Functions.md)

* Core Functions
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

* Search & Conditionals
    * `contains(where:)`
    * `allSatisfy(_:)`
    * `first(where:)`
    * `min(by:)`, `max(by:)`
    * `prefix(while:)`
    * `drop(while:)`

* Slicing
    * `prefix(_:)`, `suffix(_:)`
    * `dropFirst(_:)`, `dropLast(_:)`
    * `split(separator:)`

* Grouping & Indexing
    * `enumerated()`
    * `partition(by:)`
    * `Dictionary(grouping:by:)`
    * `Dictionary(uniqueKeysWithValues:)`

* Utility
    * `zip(_:_:)`
    * `stride(from:to:by:)`
    * `lazy`
    * `indices.map`

* Swift 5.7+ Additions
    * `chunks(ofCount:)`
    * `windows(ofCount:)`
    * `compactMapValues(_:)`
    * `sequence(first:next:)`

## [UIKit](https://github.com/Nomi-ngj/iOS_Development/blob/main/UIKit.md)

* UIViewController Lifecycle
* IBOutlets & Variables
* Constraints & AutoLayout
* UITableView & UICollectionView
* Navigation (Push, Present, Pop, Unwind)
* Storyboard vs Code

## Notifications

```swift
NotificationCenter.default.addObserver(self, selector: #selector(handleUpdate), name: .didUpdateData, object: nil)
```

## Generics

```swift
func swapValues<T>(_ a: inout T, _ b: inout T) {
    let temp = a
    a = b
    b = temp
}
```

## Memory Management

### Automatic Reference Counting (ARC)

Swift uses ARC to automatically manage memory by keeping track of how many references exist to each instance.

### Strong References

The default reference type. Increases the reference count.

```swift
class Person {
    var name: String
    init(name: String) {
        self.name = name
    }
}

var person1: Person? = Person(name: "John")
var person2 = person1
person1 = nil
// person2 still holds the object
```

### Weak References

Does not increase the reference count. Becomes `nil` automatically when the referenced object is deallocated.

```swift
class Room {
    weak var occupant: Person?
}
```

### Unowned References

Does not increase the reference count but assumes the object will always exist when accessed. Crashes if accessed after deallocation.

```swift
class Customer {
    var name: String
    var card: CreditCard?
    init(name: String) { self.name = name }
}

class CreditCard {
    unowned let customer: Customer
    init(customer: Customer) {
        self.customer = customer
    }
}
```

### Retain Cycles

Occurs when two instances hold strong references to each other.

```swift
class A {
    var b: B?
}

class B {
    var a: A?
}
```

**Fix with weak/unowned references**:

```swift
class B {
    weak var a: A?
}
```

### Closures and Retain Cycles

Closures capture variables strongly by default.

```swift
class ViewModel {
    var name = "Swift"

    lazy var printName: () -> Void = {
        [weak self] in
        print(self?.name ?? "no name")
    }
}
```

Use `[weak self]` or `[unowned self]` to prevent retain cycles.

## Swift Concurrency (async/await)

```swift
func fetchUserData() async throws -> User { ... }
```

## Error Handling

```swift
do {
    try someThrowingFunction()
} catch {
    print(error)
}
```

## Git & Source Control

* commit, push, pull, merge

## CocoaPods

```bash
pod init
pod install
```

## Design Patterns

* MVC
* MVVM

## CoreData

Apple’s built-in object graph and persistence framework.

```swift
let container = NSPersistentContainer(name: "Model")
container.loadPersistentStores { _, error in
  if let err = error { fatalError(err.localizedDescription) }
}
let context = container.viewContext

let person = PersonEntity(context: context)
person.name = "John"
try context.save()
```

## Combine

Apple’s reactive programming framework.

```swift
Just("Hello")
  .map { $0.uppercased() }
  .sink { print($0) }  // Prints "HELLO"
```

## Swift Package Manager (SPM)

```swift
let package = Package(
  name: "MyLibrary",
  products: [.library(name: "MyLibrary", targets: ["Core", "UI"])],
  targets: [...]
)
```

## Unit Testing & UI Testing

```swift
func testExample() {
  let sum = add(2, 3)
  XCTAssertEqual(sum, 5)
}
```

```swift
let app = XCUIApplication()
app.launch()
app.buttons["Login"].tap()
XCTAssert(app.staticTexts["Welcome"].exists)
```

## Localization & Accessibility

```swift
NSLocalizedString("welcome_message", comment: "")

button.accessibilityLabel = "Play"
button.accessibilityHint = "Starts the game"
```

## Architecture Patterns

* MVC
* MVVM
* VIPER
* Coordinator

## Networking & API

```swift
URLSession.shared.dataTask(with: url) { data, _, error in
  ...
}
```

* Alamofire, Moya
* Codable

## Architecture Tools

* Dependency Injection
* Protocols for Testability

## Concurrency & Threading

```swift
DispatchQueue.global().async { /* background */ }
DispatchQueue.main.async { /* UI update */ }

Task {
  let data = try await fetchData()
}
```

## Persistence & Storage

* UserDefaults
* FileManager
* Keychain
* CoreData
* Realm, SQLite

## Push Notifications

* UNUserNotificationCenter
* APNs integration

## MapKit & Location

```swift
let map = MKMapView()
map.delegate = self
map.addAnnotation(pin)
```

## SwiftUI

* `@State`, `@Binding`, `@ObservedObject`
* View Lifecycle
* Live previews

## Reactive Programming (RxSwift)

```swift
let disposeBag = DisposeBag()
Observable.just("hello")
  .subscribe(onNext: { print($0) })
  .disposed(by: disposeBag)
```

## Gesture Handling

```swift
let tap = UITapGestureRecognizer(target: self, action: #selector(tapped))
view.addGestureRecognizer(tap)
```

## Continuous Integration / CI-CD

* Fastlane
* Bitrise, CircleCI, GitHub Actions
* TestFlight
