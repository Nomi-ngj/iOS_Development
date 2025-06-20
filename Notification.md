## Notification

* Local Notifications
* Local Notification with Actions & Categories
* Push Notifications
* Silent Push Notifications
* Badge Updates
* NotificationCenter (In-App Communication)

---

## Local Notifications

You use `UNUserNotificationCenter` to schedule local notifications.

**Steps to use:**

1. Ask for permission
2. Create content
3. Create a trigger
4. Create a request
5. Add request to notification center

```swift
import UserNotifications

// Request permission
UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .sound, .badge]) { granted, error in
    if granted {
        print("Permission granted")
    } else {
        print("Permission denied")
    }
}

// Create content
let content = UNMutableNotificationContent()
content.title = "Reminder"
content.body = "Hey! Don’t forget to drink water 💧"
content.sound = .default

// Create trigger (e.g., after 5 seconds)
let trigger = UNTimeIntervalNotificationTrigger(timeInterval: 5, repeats: false)

// Create request
let request = UNNotificationRequest(identifier: UUID().uuidString, content: content, trigger: trigger)

// Schedule it
UNUserNotificationCenter.current().add(request)
```

---

## Local Notification with Actions & Categories

You can add actionable buttons to your local notifications using `UNNotificationAction` and `UNNotificationCategory`.

```swift
// Define actions
let acceptAction = UNNotificationAction(identifier: "ACCEPT_ACTION", title: "Accept", options: .foreground)
let declineAction = UNNotificationAction(identifier: "DECLINE_ACTION", title: "Decline", options: .destructive)

// Define category
let category = UNNotificationCategory(identifier: "MEETING_INVITE", actions: [acceptAction, declineAction], intentIdentifiers: [], options: [])

// Register the category
UNUserNotificationCenter.current().setNotificationCategories([category])

// Create content with category
let content = UNMutableNotificationContent()
content.title = "Team Meeting"
content.body = "Would you like to join the meeting at 3 PM?"
content.sound = .default
content.categoryIdentifier = "MEETING_INVITE"

// Trigger and request
let trigger = UNTimeIntervalNotificationTrigger(timeInterval: 10, repeats: false)
let request = UNNotificationRequest(identifier: UUID().uuidString, content: content, trigger: trigger)

UNUserNotificationCenter.current().add(request)
```

Implement delegate to handle actions:

```swift
extension AppDelegate: UNUserNotificationCenterDelegate {
    func userNotificationCenter(_ center: UNUserNotificationCenter, didReceive response: UNNotificationResponse, withCompletionHandler completionHandler: @escaping () -> Void) {
        switch response.actionIdentifier {
        case "ACCEPT_ACTION":
            print("User accepted the invite")
        case "DECLINE_ACTION":
            print("User declined the invite")
        default:
            break
        }
        completionHandler()
    }
}
```

---

## Push Notifications

Push notifications are delivered by Apple Push Notification service (APNs). You usually use this in combination with a backend server.

**Setup includes:**

* Configuring capabilities in Xcode
* Registering for remote notifications
* Implementing delegate methods to receive tokens and handle incoming notifications

```swift
// Registering
UIApplication.shared.registerForRemoteNotifications()

// Getting device token
func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
    let tokenString = deviceToken.map { String(format: "%02x", $0) }.joined()
    print("Device Token: \(tokenString)")
}

// Handling failure
func application(_ application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: Error) {
    print("Failed to register: \(error.localizedDescription)")
}
```

---

## Silent Push Notifications

Silent notifications allow your app to update content in the background without alerting the user.

**APNs Payload Example:**

```json
{
  "aps": {
    "content-available": 1
  },
  "data": {
    "type": "sync"
  }
}
```

**Enable Background Modes in Xcode:**

* Background fetch
* Remote notifications

**Handle in AppDelegate:**

```swift
func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable: Any],
                 fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
    // Handle background data fetch
    print("Received silent push with data: \(userInfo)")
    completionHandler(.newData)
}
```

---

## Badge Updates

You can update the app icon badge programmatically:

```swift
UIApplication.shared.applicationIconBadgeNumber = 5
```

To reset:

```swift
UIApplication.shared.applicationIconBadgeNumber = 0
```

To include badge value in notification:

```swift
let content = UNMutableNotificationContent()
content.title = "New Message"
content.body = "You have unread messages."
content.badge = 1
```

---

## NotificationCenter (In-App Communication)

Use `NotificationCenter` to post and observe in-app events.

### ✅ Example: Notify Payment Expired across multiple view controllers

**Step 1: Define a custom notification name**

```swift
extension Notification.Name {
    static let paymentExpired = Notification.Name("paymentExpired")
}
```

**Step 2: Post the notification (from anywhere, e.g., API failure handler)**

```swift
NotificationCenter.default.post(name: .paymentExpired, object: nil)
```

**Step 3: Observe the notification in any controller**

```swift
override func viewDidLoad() {
    super.viewDidLoad()
    NotificationCenter.default.addObserver(self, selector: #selector(handlePaymentExpired), name: .paymentExpired, object: nil)
}

@objc func handlePaymentExpired() {
    let alert = UIAlertController(title: "Session Ended", message: "Your payment session has expired.", preferredStyle: .alert)
    alert.addAction(UIAlertAction(title: "OK", style: .default))
    present(alert, animated: true)
}

// Remove observer on deinit
deinit {
    NotificationCenter.default.removeObserver(self, name: .paymentExpired, object: nil)
}
```

> Now whenever `.paymentExpired` is posted, all controllers observing it will respond accordingly.

---
