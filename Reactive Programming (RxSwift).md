
# Reactive Programming (RxSwift)

RxSwift is a framework for reactive programming in Swift. It enables composing asynchronous and event-based code using observable sequences.

* What is Reactive Programming?
* What is RxSwift?
* Core Concepts
    * Observables
    * Observers
    * Subjects
    * Disposables
    * Schedulers
* Creating Observables
* Subscribing to Observables
* Disposing Subscriptions
* Using Subjects
    * PublishSubject
    * BehaviorSubject
    * ReplaySubject
    * AsyncSubject
* Operators
    * map, flatMap, filter, debounce, merge, combineLatest, etc.
* Chaining Operators
* Error Handling
* Threading with Schedulers
* RxCocoa Integration
* MVVM with RxSwift
* Best Practices

---

## What is Reactive Programming?

Reactive Programming is a declarative programming paradigm focused on data streams and the propagation of change. It's ideal for managing asynchronous events such as user input, network responses, etc.

---

## What is RxSwift?

RxSwift is the Swift implementation of Reactive Extensions. It allows composing asynchronous operations using observable sequences.

---

## Core Concepts

### Observables

An observable emits events over time.

```swift
let observable = Observable.of(1, 2, 3)
```

### Observers

Subscribe to an observable to react to events.

```swift
observable.subscribe { event in
    print(event)
}
```

### Disposables

Manage the lifecycle of subscriptions.

```swift
let disposable = observable.subscribe(...)
disposable.dispose()
```

### Subjects

Subjects are both observable and observer.

```swift
let subject = PublishSubject<String>()
subject.onNext("Hello")
```

---

## Common Subject Types

### PublishSubject

Starts empty and emits only new elements.

```swift
let publish = PublishSubject<String>()
publish.onNext("Hi")
```

### BehaviorSubject

Requires an initial value and replays it to new subscribers.

```swift
let behavior = BehaviorSubject(value: "Initial")
behavior.onNext("Updated")
```

### ReplaySubject

Replays a buffer of elements to new subscribers.

```swift
let replay = ReplaySubject<String>.create(bufferSize: 2)
```

### AsyncSubject

Emits only the last value upon completion.

---

## Chaining Operators

```swift
Observable.of(1, 2, 3)
    .map { $0 * 2 }
    .filter { $0 > 2 }
    .subscribe(onNext: { print($0) })
```

---

## Error Handling

```swift
Observable<String>.create { observer in
    observer.onError(MyError.someError)
    return Disposables.create()
}
```

---

## Threading with Schedulers

```swift
observable
    .subscribeOn(ConcurrentDispatchQueueScheduler(qos: .background))
    .observeOn(MainScheduler.instance)
```

---

## RxCocoa Integration

Use `rx` extensions for UI bindings.

```swift
textField.rx.text
    .bind(to: viewModel.inputText)
    .disposed(by: disposeBag)
```

---

## MVVM with RxSwift

RxSwift fits naturally in MVVM, especially for input/output bindings in the `ViewModel`.

---

## Best Practices

- Use `DisposeBag` to manage memory.
- Keep business logic in `ViewModel`.
- Prefer `Driver`, `ControlProperty`, and `Signal` from RxCocoa for UI bindings.
- Avoid force unwrapping and side effects in chains.

---

> RxSwift is powerful, but should be used wisely. Use it where it adds clarity and maintainability.
