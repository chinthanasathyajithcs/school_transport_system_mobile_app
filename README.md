# 🚌 Ride Safe - School Transport Tracking App

Ride Safe is a comprehensive Flutter-based mobile application designed to bridge the communication gap between parents, school van drivers, and vehicle owners. It provides real-time GPS tracking, attendance management, and secure communication for school transportation.

## ✨ Key Features

### 👤 For Parents
* **Real-time Tracking:** Track the exact location of the school van on a live map.
* **Child Management:** Add multiple children and assign them to specific vans.
* **Attendance Notifications:** Receive instant alerts when your child boards or drops off.
* **Secure Payments:** Handle transport fee payments directly through the app.

### 🚐 For Drivers
* **Interactive Dashboard:** Manage daily routes, assigned students, and notices.
* **Live Location Sharing:** Broadcast real-time location using Mapbox integration.
* **Digital Attendance:** Mark student attendance with a simple tap.
* **Payment Tracking:** Monitor pending and completed payments from parents.

### 🏢 For Vehicle Owners
* **Fleet Management:** Register and manage multiple transport vehicles.
* **Driver Assignment:** Assign drivers to specific vehicles efficiently.
* **Vehicle Insights:** Track vehicle details and operational status.

## 🛠️ Technology Stack
* **Framework:** Flutter (Dart)
* **Backend:** Firebase (Authentication, Firestore, Realtime Database, Cloud Storage)
* **Maps & Location:** Mapbox, Google Maps Flutter, Geolocator
* **State Management:** Provider / setState

## 🏗️ Application Architecture & Software Design

### High-level Overview
Ride Safe is structured as a modular Flutter app separating UI, services, and data layers. The app supports three primary user roles — Parents, Drivers, and Vehicle Owners — each with dedicated screens and flows found under `lib/` (for example `driver_home.dart`, `vehicle_owner_home.dart`, `c_home_page.dart`). Core responsibilities are delegated to small, focused services under `lib/services/` (`auth_service.dart`, `location_service.dart`, `notification_service.dart`, `vehicle_service.dart`).

### Core Modules
- **Presentation Layer:** Stateless/Stateful widgets and screens under `lib/` and `lib/widgets/`. UI widgets are lightweight; business logic is kept out of widgets when feasible.
- **Services Layer:** Single-responsibility services encapsulate API calls, Firebase interactions, location updates, and notifications.
- **Data Layer:** Firestore/Realtime Database models and local caching (where applicable) provide data persistence and offline resilience.
- **Integration Layer:** Map integrations (Mapbox/Google Maps) and platform channels live in `mapbox_config.dart` and platform config files.

### Data Flow & State
- The app uses simple, predictable state patterns (local `setState` and lightweight Provider patterns where shared state is required). Services expose streams or Futures to keep UI reactive and testable.
- Authentication state (Firebase Auth) is the single source of truth for user sessions; user profiles and related data are stored in Firestore and referenced by document IDs.

### Error Handling & Reliability
- All external calls (Firebase, Mapbox, HTTP) use centralized error handling: catch, map to user-friendly messages, and surface retry options where appropriate.
- Location updates are rate-limited and debounced in `location_service.dart` to conserve battery and reduce costs.

### Security & Secrets Management
- Secrets and keys are loaded from environment configuration at runtime and kept out of source control. Example files such as `mapbox.env.example.json` remain in the repo as templates.
- Network calls use HTTPS and validate responses before persisting data.

## 🧰 Technologies & Lessons Learned

### Technologies Used
- **Flutter & Dart:** Cross-platform UI framework used to build a single codebase for Android, iOS, web, and desktop.
- **Firebase:** Authentication, Firestore, Realtime Database, Cloud Storage for user data, real-time updates, and file uploads.
- **Mapbox & Google Maps Flutter:** Map rendering and route/marker management. Mapbox is used for live tracking features.
- **Geolocator:** Device location handling and permissions.
- **HTTP & Cloud Functions :** For server-side logic and secure token exchanges.

### Engineering Lessons & Best Practices
- **Proper API Handling:**
   - Use service classes to encapsulate all API interactions (request/response mapping, retries, backoff).
   - Keep DTOs (data transfer objects) separate from UI models to simplify parsing and testing.
   - Validate and sanitize all incoming data from external APIs before using it in the app.

- **Authentication & Authorization:**
   - Rely on Firebase Auth for session management and security rules on Firestore to enforce access controls.
   - Avoid embedding tokens client-side; exchange short-lived tokens via secure endpoints when necessary.

- **Offline & Sync Considerations:**
   - Prefer Firestore caching and local persistence for critical reads to keep the UI responsive when offline.
   - Implement conflict resolution strategies for concurrent updates (last-writer-wins or server-side merges).


- **Performance & UX:**
   - Debounce location updates and reduce map redraws to improve battery life.
   - Load lists with pagination or lazy loading to avoid large memory spikes on low-end devices.

---

> **Note:** _This project was developed by the project team as part of the Computing Group Project module for academic assessment. The project topic and implementation were selected and completed by the team to satisfy the module requirements._


