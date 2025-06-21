# MapKit & Location

* Introduction to CoreLocation & MapKit
* Requesting Location Permissions
* Checking Location Services
* Getting the User’s Location
* Displaying Location on Map
* Customizing Annotations
* Handling Location Updates
* Best Practices

## Introduction to CoreLocation & MapKit

- **CoreLocation**: Used to get the device’s geographic location.
- **MapKit**: Used to display maps, pins, and overlays.


## Requesting Location Permissions

Update your **Info.plist**:

```xml
<key>NSLocationWhenInUseUsageDescription</key>
<string>This app needs access to your location</string>
<key>NSLocationAlwaysAndWhenInUseUsageDescription</key>
<string>This app uses your location to provide better services</string>
```

---

## Checking Location Services

```swift
import CoreLocation

let locationManager = CLLocationManager()

if CLLocationManager.locationServicesEnabled() {
    locationManager.delegate = self
    locationManager.desiredAccuracy = kCLLocationAccuracyBest
    locationManager.requestWhenInUseAuthorization()
    locationManager.startUpdatingLocation()
} else {
    print("Location services are not enabled")
}
```

---

## Getting User’s Location

```swift
func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
    if let location = locations.first {
        print("User location: \(location.coordinate.latitude), \(location.coordinate.longitude)")
    }
}
```

---

## Displaying Location on Map

```swift
import MapKit

let mapView = MKMapView(frame: view.bounds)
view.addSubview(mapView)

let coordinate = CLLocationCoordinate2D(latitude: 24.7136, longitude: 46.6753)
let region = MKCoordinateRegion(center: coordinate, latitudinalMeters: 1000, longitudinalMeters: 1000)
mapView.setRegion(region, animated: true)
```

---

## Customizing Annotations

```swift
let annotation = MKPointAnnotation()
annotation.coordinate = coordinate
annotation.title = "Riyadh"
annotation.subtitle = "Capital of Saudi Arabia"
mapView.addAnnotation(annotation)
```

---

## Handling Location Updates

Don't forget to handle errors and stop updates when done:

```swift
func locationManager(_ manager: CLLocationManager, didFailWithError error: Error) {
    print("Failed to find user's location: \(error.localizedDescription)")
}

func stopLocationUpdates() {
    locationManager.stopUpdatingLocation()
}
```

---

## Best Practices

- Always check for permission status before accessing location.
- Minimize battery use by stopping updates when not needed.
- Clearly explain why you need location data in the app.
