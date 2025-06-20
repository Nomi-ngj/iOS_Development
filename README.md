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

## Higher Order Functions

### map

```swift
let numbers = [1, 2, 3, 4]
let squared = numbers.map { $0 * $0 } // [1, 4, 9, 16]
```

### filter

```swift
let evenNumbers = numbers.filter { $0 % 2 == 0 } // [2, 4]
```

### reduce

```swift
let sum = numbers.reduce(0, +) // 10
```

### compactMap

```swift
let values = ["1", "two", "3"]
let validInts = values.compactMap { Int($0) } // [1, 3]
```

### flatMap

```swift
let nested = [[1, 2], [3, 4], [5, 6]]
let flattened = nested.flatMap { $0 } // [1, 2, 3, 4, 5, 6]
```

### forEach

```swift
numbers.forEach { print($0) }
```

### sorted

```swift
let sorted = numbers.sorted(by: >) // [4, 3, 2, 1]
```

### zip

```swift
let names = ["Alice", "Bob", "Charlie"]
let scores = [85, 92, 78]
let zipped = Array(zip(names, scores))
// [("Alice", 85), ("Bob", 92), ("Charlie", 78)]
```

### first(where:)

```swift
let firstEven = numbers.first(where: { $0 % 2 == 0 }) // 2
```

### dropFirst / dropLast

```swift
let droppedFirst = numbers.dropFirst() // [2, 3, 4]
let droppedLast = numbers.dropLast()   // [1, 2, 3]
```

### prefix / suffix

```swift
let firstTwo = numbers.prefix(2) // [1, 2]
let lastTwo = numbers.suffix(2)  // [3, 4]
```

### group(by:) using Dictionary

```swift
let names = ["Anna", "Alex", "Brian", "Bob"]
let grouped = Dictionary(grouping: names) { $0.first! }
// ["A": ["Anna", "Alex"], "B": ["Brian", "Bob"]]
```

### allSatisfy

```swift
let allPositive = numbers.allSatisfy { $0 > 0 } // true
```

### contains(where:)

```swift
let hasNegative = numbers.contains(where: { $0 < 0 }) // false
```

### enumerated

```swift
for (index, value) in numbers.enumerated() {
    print("\(index): \(value)")
}
```

### partition

```swift
var values = [10, 20, 5, 8, 15]
let pivot = values.partition { $0 >= 10 }
// values: [5, 8, 20, 10, 15], pivot: 2
```

### joined

```swift
let words = [["Hello"], ["World"]]
let flat = words.joined() // ["Hello", "World"]
```

### reduce(into:)

```swift
let result = numbers.reduce(into: []) { $0.append($1 * 2) } // [2, 4, 6, 8]
```

### reversed

```swift
let reversed = numbers.reversed() // [4, 3, 2, 1]
```

### split

```swift
let sentence = "This is a test"
let words = sentence.split(separator: " ") // ["This", "is", "a", "test"]
```

### shuffle / shuffled

```swift
let shuffled = numbers.shuffled() // Random order
```

### min / max

```swift
let smallest = numbers.min() // 1
let largest = numbers.max()  // 4
```

### drop(while:)

```swift
let result = numbers.drop(while: { $0 < 3 }) // [3, 4]
```

### prefix(while:) / suffix(while:) (Swift 5.1+)

```swift
let prefixResult = numbers.prefix(while: { $0 < 3 }) // [1, 2]
```

### lazy

```swift
let lazyMapped = numbers.lazy.map { $0 * 2 }
```

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

Use either or both depending on project needs.


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
