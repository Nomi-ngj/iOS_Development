# SwiftUI

SwiftUI is Apple’s modern framework for building declarative user interfaces across all Apple platforms using Swift.

1. What is SwiftUI?
2. SwiftUI vs UIKit
3. Basic Components
4. Layout System
5. State Management
6. View Lifecycle
7. SwiftUI Macros (Swift 5.9 / Swift 6+)
8. Navigation
9. Animations
10. SwiftUI and Combine
11. Previews
12. Integration with UIKit
13. Best Practices


## 1. What is SwiftUI?

SwiftUI is a declarative UI framework introduced by Apple that enables developers to design UI using Swift syntax.


## 2. SwiftUI vs UIKit

| Feature         | SwiftUI                          | UIKit                            |
|----------------|----------------------------------|----------------------------------|
| Style          | Declarative                      | Imperative                       |
| Cross-platform | Yes                              | No                               |
| Previews       | Yes (live preview)               | No                               |
| Code Concise   | Highly concise                   | Verbose                          |

---

## 3. Basic Components

```swift
Text("Hello, SwiftUI!")
Button("Tap Me") { print("Tapped!") }
Image(systemName: "star.fill")
```

---

## 4. Layout System

```swift
VStack {
    Text("Top")
    Spacer()
    Text("Bottom")
}
.padding()
```

Layouts: `VStack`, `HStack`, `ZStack`, `Spacer`, `GeometryReader`, `Grid` (iOS 16+)

---

## 5. State Management

- `@State`
- `@Binding`
- `@ObservedObject`
- `@EnvironmentObject`
- `@StateObject`

```swift
@State private var count = 0

Button("Tap") {
    count += 1
}
```

---

## 6. View Lifecycle

SwiftUI uses declarative lifecycle:
- `onAppear`
- `onDisappear`

---

## 7. SwiftUI Macros (Swift 5.9 / Swift 6+)

- `#Preview`
- `#Observable`
- `#Bindable`

```swift
#Observable
class Counter {
    var count = 0
}

#Preview {
    CounterView()
}
```

---

## 8. Navigation

```swift
NavigationStack {
    NavigationLink("Go to Detail", destination: Text("Detail View"))
}
```

---

## 9. Animations

```swift
@State private var isFlipped = false

Image("card")
    .rotation3DEffect(.degrees(isFlipped ? 180 : 0), axis: (x: 0, y: 1, z: 0))
    .onTapGesture {
        withAnimation {
            isFlipped.toggle()
        }
    }
```

---

## 10. SwiftUI and Combine

Use Combine to handle events and data streams:

```swift
@ObservedObject var viewModel: SomeViewModel
```

---

## 11. Previews

```swift
struct MyView_Previews: PreviewProvider {
    static var previews: some View {
        MyView()
    }
}
```

Use `#Preview` for modern macro-based previews.

---

## 12. Integration with UIKit

```swift
struct UIKitView: UIViewControllerRepresentable {
    func makeUIViewController(context: Context) -> UIViewController {
        return MyUIKitViewController()
    }

    func updateUIViewController(_ uiViewController: UIViewController, context: Context) {}
}
```

---

## 13. Best Practices

- Use small reusable views
- Leverage property wrappers properly
- Avoid deep view hierarchies
- Prefer structs and lightweight models

---

> SwiftUI evolves rapidly, especially with newer Swift versions. Keep your tools and Xcode updated for access to the latest features.
