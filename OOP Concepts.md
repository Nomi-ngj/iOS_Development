 OOP Concepts
---
### Inheritance

Inheritance allows a class to inherit properties and methods from another class.

```swift
class Animal {
    func speak() {
        print("Animal speaks")
    }
}

class Dog: Animal {
    override func speak() {
        print("Dog barks")
    }
}

let myDog = Dog()
myDog.speak() // Output: Dog barks
```

### Polymorphism

Polymorphism allows methods to behave differently based on the object calling them.

```swift
class Animal {
    func makeSound() {
        print("Some sound")
    }
}

class Cat: Animal {
    override func makeSound() {
        print("Meow")
    }
}

class Cow: Animal {
    override func makeSound() {
        print("Moo")
    }
}

let animals: [Animal] = [Cat(), Cow()]
for animal in animals {
    animal.makeSound()
}
// Output:
// Meow
// Moo
```

### Encapsulation

Encapsulation hides internal data and only exposes necessary parts.

```swift
class BankAccount {
    private var balance: Double = 0.0

    func deposit(amount: Double) {
        if amount > 0 {
            balance += amount
        }
    }

    func getBalance() -> Double {
        return balance
    }
}

let account = BankAccount()
account.deposit(amount: 1000)
print(account.getBalance()) // Output: 1000.0
```

### Abstraction

Abstraction hides complexity by exposing only essential features.

```swift
protocol Vehicle {
    func start()
    func stop()
}

class Car: Vehicle {
    func start() {
        print("Car started")
    }

    func stop() {
        print("Car stopped")
    }
}

func operateVehicle(_ vehicle: Vehicle) {
    vehicle.start()
    vehicle.stop()
}

let myCar = Car()
operateVehicle(myCar)
// Output:
// Car started
// Car stopped
```
