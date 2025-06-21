# Architecture Patterns

* MVC (Model-View-Controller)
* MVVM (Model-View-ViewModel)
* VIPER
* Coordinator
* [Clean Architecture](https://github.com/Nomi-ngj/iOS_Development/blob/main/Clean%20Architecture.md)

## MVC (Model-View-Controller)

**MVC** separates your app logic into:

- **Model**: Data and business logic
- **View**: UI elements
- **Controller**: Mediator between Model and View

### Example:

```swift
class UserModel {
    var name: String
    init(name: String) { self.name = name }
}

class UserView: UIView {
    let nameLabel = UILabel()
}

class UserController: UIViewController {
    let model = UserModel(name: "Nouman")
    let userView = UserView()

    override func viewDidLoad() {
        super.viewDidLoad()
        userView.nameLabel.text = model.name
    }
}
```

---

## MVVM (Model-View-ViewModel)

**MVVM** promotes separation by introducing a **ViewModel** that prepares data for the View.

### Example:

```swift
struct User {
    let name: String
}

class UserViewModel {
    private let user: User
    var displayName: String { "Name: \(user.name)" }

    init(user: User) {
        self.user = user
    }
}

class UserViewController: UIViewController {
    let viewModel = UserViewModel(user: User(name: "Nouman"))

    override func viewDidLoad() {
        super.viewDidLoad()
        print(viewModel.displayName)
    }
}
```

---

## VIPER

**VIPER** breaks down responsibilities into 5 components:

- **View**
- **Interactor**
- **Presenter**
- **Entity**
- **Router**

Each has a single responsibility. Common in large, testable applications.

### Basic Structure:

```swift
protocol PresenterToView {
    func showData(_ data: String)
}

class View: PresenterToView {
    var presenter: ViewToPresenter!
    func showData(_ data: String) {
        print("Display: \(data)")
    }
}
```

---

## Coordinator

**Coordinator Pattern** is used to manage navigation logic outside of view controllers.

### Example:

```swift
protocol Coordinator {
    var navigationController: UINavigationController { get set }
    func start()
}

class MainCoordinator: Coordinator {
    var navigationController: UINavigationController

    init(navController: UINavigationController) {
        self.navigationController = navController
    }

    func start() {
        let vc = UIViewController()
        navigationController.pushViewController(vc, animated: true)
    }
}
```

## Clean Architecture

```
Entities → Use Cases → Interface Adapters → Frameworks & Drivers
```

Folder Structure Example

```
MyApp/
├── Entities/
├── UseCases/
├── InterfaceAdapters/
│   ├── ViewModels/
│   └── Presenters/
├── Frameworks/
│   ├── UI/
│   └── Network/
└── App/
    └── AppDelegate.swift
```

This promotes reusability and separation of concerns, especially in navigation-heavy apps.
