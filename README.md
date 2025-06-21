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

## [Notification](https://github.com/Nomi-ngj/iOS_Development/blob/main/Notification.md)

* Local Notifications
* Local Notification with Actions & Categories
* Push Notifications
* Silent Push Notifications
* Badge Updates
* NotificationCenter (In-App Communication)

## [Generics](https://github.com/Nomi-ngj/iOS_Development/blob/main/Generics.md)

* What are Generics?
* Basic Generic Function
* Generic Types (Structs, Classes, Enums)
* Generic Constraints
* Associated Types in Protocols
* Advanced: Generic Protocol Extensions
* Advanced: Type Erasure with Generics
* Benefits

## [Memory Management in Swift](https://github.com/Nomi-ngj/iOS_Development/blob/main/Memory%20Management.md)

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

## [Git & Source Control](https://github.com/Nomi-ngj/iOS_Development/blob/main/Git%20%26%20Source%20Control.md)

* What is Git?
* Basic Git Workflow
* Common Git Commands
* Branching Strategy
    * `main` branch
    * `develop` branch
    * `feature` branches
    * `task` branches
* Working with Remotes
* Best Practices

## [CocoaPods](https://github.com/Nomi-ngj/iOS_Development/blob/main/CocoaPods.md)

- What is CocoaPods?
- Installing CocoaPods
- Setting Up CocoaPods in a Project
- Adding Dependencies
- Using Pod Commands
- Updating and Removing Pods
- Best Practices

## [Swift Package Manager (SPM)](https://github.com/Nomi-ngj/iOS_Development/blob/main/Swift%20Package%20Manager%20(SPM).md)

- What is Swift Package Manager?
- Benefits of Using SPM
- Creating a Swift Package
- Adding Dependencies
- Using Packages in Xcode
- Common Commands
- Best Practices


## [Design Patterns](https://github.com/Nomi-ngj/iOS_Development/blob/main/Design%20Patterns.md)

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

## Persistence & Storage

* UserDefaults
* FileManager
* Keychain
* CoreData
* Realm, SQLite

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
