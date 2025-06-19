# Objective-C: Apple’s Legacy Language for iOS/macOS

**Objective-C** is a powerful, object-oriented programming language built on top of C. It adds **dynamic messaging**, **runtime flexibility**, and **object-oriented patterns** that are key to developing apps in Apple’s ecosystem.

It was the **main language for macOS and iOS** development until the release of [Swift](https://developer.apple.com/swift/), and is still widely used in enterprise and legacy codebases.

---

## Key Characteristics

* **Superset of C**: All valid C code is valid Objective-C code.
* **Dynamic Runtime**: Messages are resolved at runtime (unlike C++).
* **Messaging Syntax**: Uses `[receiver message]` instead of dot syntax.
* **Foundation Framework**: Includes powerful base types like `NSString`, `NSArray`, `NSDictionary`, etc.
* **Interoperability**: Can work seamlessly with Swift using bridging headers.

---

## Syntax Basics

### Class Interface and Implementation

```objc
// Interface (.h file)
@interface Person : NSObject
@property (nonatomic, strong) NSString *name;
- (void)sayHello;
@end

// Implementation (.m file)
@implementation Person
- (void)sayHello {
    NSLog(@"Hello, my name is %@", self.name);
}
@end
```

### Using the Class

```objc
Person *p = [[Person alloc] init];
p.name = @"Nouman";
[p sayHello]; // Output: Hello, my name is Nouman
```

---

## Common Concepts

### Properties

```objc
@property (nonatomic, strong) NSString *name;
```

* `nonatomic` – non-thread-safe but faster
* `strong`, `weak`, `copy`, `assign` – memory attributes

### Methods

```objc
- (void)doSomething;
+ (instancetype)createObject;
```

* `-` means instance method
* `+` means class/static method

### Message Passing

```objc
[object doSomething];
```

Unlike method calls in C++ or Swift, this is **runtime message dispatching**.

---

## Memory Management

Objective-C uses **Automatic Reference Counting (ARC)** like Swift.

```objc
__strong // default, retains ownership
__weak   // does not retain
__unsafe_unretained // like weak but doesn't nil out
```

---

## Bridging with Swift

In mixed projects, use a **Bridging Header** to call Objective-C code from Swift and vice versa.

```swift
// Swift
let person = Person()
person.name = "Ali"
person.sayHello()
```

---

## Useful Resources

* [Apple Docs – Objective-C](https://developer.apple.com/documentation/objectivec)
* [Programming with Objective-C](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/)
* [RayWenderlich Obj-C Tutorials](https://www.raywenderlich.com/ios/paths/learn)

---

## When to Use Objective-C Today?

* Maintaining or integrating with **legacy apps**
* Building **Cocoa/Cocoa Touch** extensions
* When using **runtime features** like method swizzling
* Interacting with **C APIs or libraries**

---

## Example: Category (Extend Class Behavior)

```objc
@interface NSString (Reverse)
- (NSString *)reversedString;
@end

@implementation NSString (Reverse)
- (NSString *)reversedString {
    NSMutableString *result = [NSMutableString stringWithCapacity:self.length];
    for (NSInteger i = self.length - 1; i >= 0; i--) {
        [result appendFormat:@"%C", [self characterAtIndex:i]];
    }
    return result;
}
@end
```

---

> *Objective-C is the foundation of Apple’s ecosystem. Learning it gives you a deeper understanding of how iOS/macOS work under the hood.*
