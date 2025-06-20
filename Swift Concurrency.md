
## Swift Concurrency


1. `async / await`
2. `Task {}` – Unstructured Task
3. `Task.detached` – Detached Task
4. `async let` – Parallel Async Bindings
5. `TaskGroup` – Structured Concurrency
6. `@MainActor` – UI Thread Execution
7. `actor` – Isolated State Object
8. `Task.cancel()` – Cooperative Cancellation

---

### 1. `async / await`

**What it does**: Asynchronous call with suspension  
**When to use**: Any non-blocking I/O operations

```swift
try await fetch()
```

---

### 2. `Task {}`

**What it does**: Creates an unstructured task that inherits actor/priority  
**When to use**: Background operations from UI code

```swift
Task {
    await load()
}
```

---

### 3. `Task.detached`

**What it does**: Runs a task outside the current actor context  
**When to use**: Work-items without access to local state

```swift
Task.detached {
    await heavy()
}
```

---

### 4. `async let`

**What it does**: Parallel request with automatic await  
**When to use**: Parallel execution of known operations

```swift
async let a = slowA()
async let b = slowB()
let res = await (a, b)
```

---

### 5. `TaskGroup`

**What it does**: Dynamic number of child tasks  
**When to use**: Fan-out / result aggregation

```swift
await withTaskGroup(of: Void.self) { group in
    group.addTask {
        await work()
    }
}
```

---

### 6. `@MainActor`

**What it does**: Guarantees execution on the main thread  
**When to use**: UI updates, no need for `DispatchQueue.main`

```swift
@MainActor
func updateUI() {
    // UI code here
}
```

---

### 7. `actor`

**What it does**: Defines an isolated state object  
**When to use**: Thread-safe caches, services

```swift
actor Cache {
    var store = [String: Data]()
}
```

---

### 8. `Task.cancel()`

**What it does**: Cooperative cancellation of async work  
**When to use**: Long-running operations that may need cancellation

```swift
if Task.isCancelled {
    return
}
```
