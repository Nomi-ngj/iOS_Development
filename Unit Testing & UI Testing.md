
# Unit Testing & UI Testing

* What is Unit Testing?
* What is UI Testing?
* XCTest Framework
* Writing Unit Tests
* Writing UI Tests
* Mocking & Dependency Injection
* Code Coverage
* Best Practices

## What is Unit Testing?

Unit testing verifies that individual components (functions, classes) of your code behave as expected.


## What is UI Testing?

UI testing ensures that the UI behaves correctly through simulated user interaction (buttons, navigation, etc.).


## XCTest Framework

XCTest is Apple’s official framework for writing unit and UI tests in Swift.

```swift
import XCTest
```

---

## Writing Unit Tests

```swift
import XCTest
@testable import MyApp

class MyAppTests: XCTestCase {

    func testAddition() {
        let result = 2 + 2
        XCTAssertEqual(result, 4)
    }
}
```

---

## Writing UI Tests

```swift
import XCTest

class MyAppUITests: XCTestCase {

    func testLoginButton() {
        let app = XCUIApplication()
        app.launch()
        app.buttons["Login"].tap()
        XCTAssert(app.textFields["Email"].exists)
    }
}
```

---

## Mocking & Dependency Injection

Mock dependencies to isolate components during testing.

```swift
protocol NetworkService {
    func fetchData() -> String
}

class MockService: NetworkService {
    func fetchData() -> String {
        return "Mocked"
    }
}
```

---

## Code Coverage

Check which parts of your code are tested:

* Product → Scheme → Edit Scheme → Test → Options → Enable Code Coverage

---

## Best Practices

* Test one thing per test.
* Use descriptive test function names.
* Clean up in `tearDown()`.
* Avoid relying on order of tests.
* Keep tests fast and isolated.

---

## 🛠️ Tools

* `Quick` and `Nimble`: BDD-style testing frameworks.
* `SnapshotTesting`: Validate UI appearance.
