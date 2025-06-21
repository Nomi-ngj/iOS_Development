
# Persistence & Storage

iOS provides various mechanisms to store data persistently on the device. Here's an overview with examples.

* UserDefaults
* FileManager
* Keychain
* CoreData
* Realm, SQLite


## UserDefaults

Use `UserDefaults` to store small pieces of data like user settings.

```swift
UserDefaults.standard.set("John", forKey: "username")
let username = UserDefaults.standard.string(forKey: "username")
```

---

## FileManager

Use `FileManager` for reading/writing files to disk.

```swift
let fileName = "example.txt"
if let dir = FileManager.default.urls(for: .documentDirectory, in: .userDomainMask).first {
    let fileURL = dir.appendingPathComponent(fileName)
    do {
        try "Hello, File!".write(to: fileURL, atomically: false, encoding: .utf8)
        let content = try String(contentsOf: fileURL)
    } catch {
        print("File error: \(error)")
    }
}
```

---

## Keychain

Use Keychain to securely store sensitive data like passwords or tokens.

```swift
import Security

func saveToKeychain(value: String, forKey key: String) {
    let data = value.data(using: .utf8)!
    let query: [String: Any] = [
        kSecClass as String: kSecClassGenericPassword,
        kSecAttrAccount as String: key,
        kSecValueData as String: data
    ]
    SecItemAdd(query as CFDictionary, nil)
}
```

---

## CoreData

Use CoreData for complex object graphs and relationships.

```swift
// Define NSManagedObject
class Person: NSManagedObject {
    @NSManaged var name: String?
}

// Save object
let person = Person(context: context)
person.name = "Alice"
try? context.save()
```

---

## Realm & SQLite

### Realm
Realm is a third-party mobile database.

```swift
let person = Person()
person.name = "John"
let realm = try! Realm()
try! realm.write {
    realm.add(person)
}
```

### SQLite
Use SQLite.swift or similar wrapper for interacting with SQLite.

```swift
import SQLite

let db = try Connection("path/to/db.sqlite3")
let users = Table("users")
let name = Expression<String>("name")

try db.run(users.insert(name <- "Alice"))
```

---

> Choose the right storage mechanism based on your data type, sensitivity, and persistence needs.
