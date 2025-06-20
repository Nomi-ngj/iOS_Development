
# CocoaPods in iOS

CocoaPods is a dependency manager for Swift and Objective-C Cocoa projects. It helps you manage third-party libraries and frameworks in a standardized way.


## Index

- What is CocoaPods?
- Installing CocoaPods
- Setting Up CocoaPods in a Project
- Adding Dependencies
- Using Pod Commands
- Updating and Removing Pods
- Best Practices


## What is CocoaPods?

CocoaPods manages library dependencies for your Xcode projects. It creates a workspace and links your dependencies automatically.


## Installing CocoaPods

```bash
sudo gem install cocoapods
```

Verify installation:

```bash
pod --version
```

---

## Setting Up CocoaPods in a Project

1. Navigate to your Xcode project directory:

```bash
cd /path/to/your/project
```

2. Initialize CocoaPods:

```bash
pod init
```

3. Open `Podfile` and add your dependencies.

---

## ➕ Adding Dependencies

Edit the `Podfile`:

```ruby
platform :ios, '13.0'
use_frameworks!

target 'YourApp' do
  pod 'Alamofire'
  pod 'Kingfisher'
end
```

Then install:

```bash
pod install
```

> Always open `.xcworkspace` after installing pods.

---

## Using Pod Commands

- `pod install` – Install pods listed in Podfile.
- `pod update` – Update all pods to latest version.
- `pod update Alamofire` – Update specific pod.
- `pod deintegrate` – Remove CocoaPods from Xcode project.
- `pod repo update` – Update local podspec repo.

---

## Updating and Removing Pods

To update all pods:

```bash
pod update
```

To remove a pod, delete the line from `Podfile` and run:

```bash
pod install
```

---

## Best Practices

- Commit `Podfile` and `Podfile.lock` to version control.
- Always open the `.xcworkspace` file.
- Avoid manual changes in `Pods/` folder.
- Keep CocoaPods updated regularly.
