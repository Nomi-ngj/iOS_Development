# Architecture Tools

- Dependency Injection
- Protocols for Testability

## Dependency Injection

Dependency Injection (DI) is a design pattern where a class receives its dependencies from external sources rather than creating them internally.

### Benefits:
- Makes code more modular and testable.
- Reduces tight coupling.
- Promotes reuse and flexibility.

### Example:

```swift
protocol APIService {
    func fetchData()
}

class RealAPIService: APIService {
    func fetchData() {
        print("Fetching from real service")
    }
}

class ViewModel {
    private let service: APIService

    init(service: APIService) {
        self.service = service
    }

    func loadData() {
        service.fetchData()
    }
}

// Injecting dependency
let viewModel = ViewModel(service: RealAPIService())
viewModel.loadData()
```

---

## Protocols for Testability

Using protocols allows you to mock or stub implementations for unit testing.

### Benefits:
- Enables mock objects for unit testing.
- Abstracts concrete implementations.

### Example:

```swift
protocol NetworkClient {
    func request(endpoint: String, completion: @escaping (String) -> Void)
}

class APIClient: NetworkClient {
    func request(endpoint: String, completion: @escaping (String) -> Void) {
        completion("Real response from \(endpoint)")
    }
}

class MockClient: NetworkClient {
    func request(endpoint: String, completion: @escaping (String) -> Void) {
        completion("Mocked response")
    }
}

class DataFetcher {
    var client: NetworkClient

    init(client: NetworkClient) {
        self.client = client
    }

    func fetch() {
        client.request(endpoint: "/data") { response in
            print(response)
        }
    }
}

// Use mock during testing
let fetcher = DataFetcher(client: MockClient())
fetcher.fetch()
```

---

## Summary

| Tool                   | Purpose                                     | Benefit                        |
|------------------------|---------------------------------------------|--------------------------------|
| Dependency Injection   | Provide dependencies from outside           | Easier testing, decoupling     |
| Protocols              | Abstract behavior for flexibility/testing   | Mocking, abstraction           |
