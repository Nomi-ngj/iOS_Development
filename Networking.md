
# Networking & API

- Introduction
- URLSession
- URLRequest
- Codable and JSONDecoder
- Using Completion Handlers
- Using async/await (Swift Concurrency)
- Alamofire (Third-party)
- Combine Framework
- Error Handling
- Best Practices

## Introduction

Networking allows iOS apps to communicate with external services via APIs (Application Programming Interfaces).

## 1. URLSession

`URLSession` is the native way to perform networking tasks.

```swift
let url = URL(string: "https://api.example.com/data")!
let task = URLSession.shared.dataTask(with: url) { data, response, error in
    if let data = data {
        print(String(data: data, encoding: .utf8)!)
    }
}
task.resume()
```

---

## 2. URLRequest

Used to configure HTTP headers, method, and body.

```swift
var request = URLRequest(url: URL(string: "https://api.example.com/login")!)
request.httpMethod = "POST"
request.setValue("application/json", forHTTPHeaderField: "Content-Type")
request.httpBody = try? JSONSerialization.data(withJSONObject: ["email": "user@example.com", "password": "123456"])
```

---

## 3. Codable and JSONDecoder

Use `Codable` to parse JSON data into Swift types.

```swift
struct User: Codable {
    let name: String
    let age: Int
}

let decoder = JSONDecoder()
let user = try decoder.decode(User.self, from: data)
```

---

## 4. Using Completion Handlers

```swift
func fetchData(completion: @escaping (Result<User, Error>) -> Void) {
    let url = URL(string: "https://api.example.com/user")!
    URLSession.shared.dataTask(with: url) { data, _, error in
        if let data = data {
            do {
                let user = try JSONDecoder().decode(User.self, from: data)
                completion(.success(user))
            } catch {
                completion(.failure(error))
            }
        }
    }.resume()
}
```

---

## 5. Using async/await (Swift Concurrency)

```swift
func fetchUser() async throws -> User {
    let url = URL(string: "https://api.example.com/user")!
    let (data, _) = try await URLSession.shared.data(from: url)
    return try JSONDecoder().decode(User.self, from: data)
}
```

---

## 6. Alamofire (Third-party)

```swift
import Alamofire

AF.request("https://api.example.com/user").responseDecodable(of: User.self) { response in
    switch response.result {
    case .success(let user):
        print(user.name)
    case .failure(let error):
        print(error)
    }
}
```

---

## 7. Combine Framework

```swift
import Combine

func fetchUserPublisher() -> AnyPublisher<User, Error> {
    let url = URL(string: "https://api.example.com/user")!
    return URLSession.shared.dataTaskPublisher(for: url)
        .map(\.data)
        .decode(type: User.self, decoder: JSONDecoder())
        .eraseToAnyPublisher()
}
```

---

## 8. Error Handling

Always handle possible errors: networking issues, decoding issues, and missing data.

```swift
enum APIError: Error {
    case invalidURL
    case decodingFailed
    case serverError
}
```

---

## 9. Best Practices

- Use `Codable` for parsing JSON.
- Modularize your networking layer.
- Centralize error handling.
- Prefer `async/await` for readability.
- Secure sensitive data (tokens, credentials).
- Use tools like Charles Proxy, Postman for testing.
