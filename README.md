# School Track — Firebase-ready Flutter MVP

This project contains the app layer for a school transport system: parent, driver and admin roles, pickup/drop requests, Firestore streams, driver GPS upload, Google Maps display and Firebase Messaging initialization.

## 1. Create Firebase project
1. Open Firebase Console and create a project.
2. Enable Authentication → Email/Password.
3. Create Firestore Database.
4. Add an Android app with package name `com.example.school_track` (or your chosen package).
5. Install FlutterFire CLI on a computer if available and run `flutterfire configure`. If you only have a phone, use the GitHub Actions route below.

## 2. Firebase data model
- `users/{uid}`: `{email, role: parent|driver|admin, name, phone}`
- `students/{studentId}`: `{name, parentUid, pickupPoint, dropPoint, status, busId}`
- `buses/{busId}`: `{busNumber, driverUid, routeName}`
- `trips/{tripId}`: `{busId, driverUid, status, location: GeoPoint, updatedAt}`
- `pickupRequests/{requestId}`: `{studentName, parentUid, pickupPoint, dropPoint, status, createdAt}`
- `notifications/{id}`: `{uid, title, body, createdAt}`

## 3. Firestore rules
Publish `firestore.rules` from Firebase Console or Firebase CLI. Do not leave Firestore in test mode for production.

## 4. Smartphone-only GitHub build
Upload the project to a private GitHub repository. Add these GitHub Actions secrets:
- `FIREBASE_OPTIONS_DART`: complete contents of the generated `lib/firebase_options.dart` from your Firebase/FlutterFire configuration.
- `MAPS_API_KEY`: your Google Maps Android API key restricted to your app.
Then open Actions → Build School Track APK → Run workflow. Download the `school-track-release-apk` artifact.

## 5. Android Firebase/FCM note
For reliable Firebase Messaging on Android, also add the Firebase Android app configuration (`google-services.json`) to the Android project when using a persistent generated Android folder. Do not publish it in a public repository. The GitHub workflow can be extended to restore it from a GitHub secret/base64 file.

## 6. Production requirements still outside source code
Real deployment needs: verified school/admin accounts, privacy/consent policy, Google Maps billing/API restrictions, Firebase billing limits, background-location policy review, device testing, crash monitoring, and secure role administration. Never put API keys or service-account credentials directly in Dart source.
