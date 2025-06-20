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

## UIKit

### UIViewController Lifecycle

Understanding the lifecycle helps in placing code appropriately.

```swift
class MyViewController: UIViewController {
    override func viewDidLoad() {
        super.viewDidLoad()
        print("View did load")
    }

    override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        print("View will appear")
    }

    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)
        print("View did appear")
    }

    override func viewWillDisappear(_ animated: Bool) {
        super.viewWillDisappear(animated)
        print("View will disappear")
    }

    override func viewDidDisappear(_ animated: Bool) {
        super.viewDidDisappear(animated)
        print("View did disappear")
    }
}
```

---

### IBOutlets

IBOutlets allow you to reference storyboard UI components in code.

```swift
class MyViewController: UIViewController {
    @IBOutlet weak var myLabel: UILabel!

    override func viewDidLoad() {
        super.viewDidLoad()
        myLabel.text = "Hello from IBOutlet!"
    }
}
```

* `@IBOutlet` connects the UI component in Interface Builder to code.
* Always marked as `weak` to avoid retain cycles.

---

### Constraints & AutoLayout

Use constraints to control layout dynamically across devices.

```swift
let label = UILabel()
label.translatesAutoresizingMaskIntoConstraints = false
view.addSubview(label)

NSLayoutConstraint.activate([
    label.centerXAnchor.constraint(equalTo: view.centerXAnchor),
    label.centerYAnchor.constraint(equalTo: view.centerYAnchor)
])
```

---

### UITableView & UICollectionView

These are used to display scrollable lists and grids.

**UITableView Example:**

```swift
class MyTableViewController: UITableViewController {
    @IBOutlet weak var tableView: UITableView!
    let items = ["Apple", "Banana", "Orange"]

    override func viewDidLoad() {
        super.viewDidLoad()
        tableView.dataSource = self
        tableView.delegate = self
    }

    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return items.count
    }

    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "Cell", for: indexPath)
        cell.textLabel?.text = items[indexPath.row]
        return cell
    }
}
```

**UICollectionView Example:**

```swift
class MyCollectionViewController: UICollectionViewController {
    @IBOutlet weak var collectionView: UICollectionView!
    let items = ["Red", "Green", "Blue"]

    override func viewDidLoad() {
        super.viewDidLoad()
        collectionView.dataSource = self
        collectionView.delegate = self
    }

    override func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int {
        return items.count
    }

    override func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "Cell", for: indexPath)
        cell.backgroundColor = .red
        return cell
    }
}
```

---

### Storyboard vs Code

**Storyboard:**

* Visual interface builder.
* Easy to prototype UI.
* Can lead to merge conflicts in team environments.

**Code:**

* Full control.
* Easier to version control.
* Preferred for complex, dynamic interfaces.

Example in Code:

```swift
let button = UIButton(type: .system)
button.setTitle("Click Me", for: .normal)
view.addSubview(button)
```


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
