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
