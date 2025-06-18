# iOS Development Concepts

## Objective-C and Swift Concepts

### Copy vs Readonly

```objc
@property (nonatomic, readonly) NSString *name; // Only getter
@property (nonatomic, copy) NSString *name; // Copies value, important for NSMutableString
```

### Copy vs Strong

```swift
class Person {
    var name: NSMutableString = "John"
}

let p1 = Person()
let p2 = p1
p2.name.append(" Smith")
print(p1.name) // "John Smith" for strong, original changes
```

### Weak vs Strong

```swift
class A {
    var b: B?
}

class B {
    weak var a: A? // Avoid retain cycle
}
```

### Weak vs Unowned

```swift
class A {
    var b: B?
}

class B {
    unowned var a: A // Must not be nil when accessed
    init(a: A) { self.a = a }
}
```

### ARC & Retain Cycle

```swift
class A {
    var b: B?
}
class B {
    var a: A? // Retain cycle if both strong
}
```

## Swift Language Fundamentals

### Optionals

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

### `lazy` Keyword

```swift
lazy var name: String = computeName()
```

### `[weak self]` & `[unowned self]`

```swift
someClosure = { [weak self] in
    self?.doSomething()
}
```

### Enums

```swift
enum Direction {
    case north, south, east, west
}
```

### `class` vs `struct`

```swift
class A {}
struct B {}
```

### Closures

```swift
let greet = { (name: String) in
    print("Hello, \(name)")
}
```

### `@escaping` & `@nonescaping`

```swift
func fetchData(completion: @escaping () -> Void) {}
```

## Swift Essentials

* Properties
* Control Flow (`if`, `for`, `while`, `switch`)
* Collections (`Array`, `Set`, `Dictionary`)
* Keywords (`let`, `var`, `in`, `is`, `as`, `defer`, `guard`)
* Functions and Parameters
* Higher Order Functions
* Access Control
* Type Casting

## OOP Concepts

* Inheritance
* Polymorphism
* Encapsulation
* Abstraction

## UIKit

* UITableView & UICollectionView
* UIViewController Lifecycle
* Constraints & AutoLayout
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

* ARC (Automatic Reference Counting)
* Strong vs Weak vs Unowned
* Retain Cycles

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

## Protocols & Delegates

```swift
protocol MyDelegate: AnyObject {
    func didUpdate()
}
```

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
