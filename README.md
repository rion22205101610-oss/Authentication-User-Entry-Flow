SmartFootball Pro: Authentication & User Entry Flow

This module serves as the primary security layer and navigation backbone of the application. It manages the entire user lifecycle—from initial branding and boot-up to persistent session monitoring and cloud-based profile synchronization.

---

System Architecture & Logic Flow

1. App Initialization (`splash_screen.dart`)
Purpose: Acts as the application's entry point to establish brand identity.
Logic: Implements a `Timer` that triggers a navigation transition after **2 seconds**.
Visuals:** Displays the "SmartFootball Pro" logo and tagline using a white-on-green high-contrast theme.

2. The Gatekeeper (`auth_gate.dart`)
Function: Uses a `StreamBuilder` to listen to `FirebaseAuth.instance.authStateChanges()`.
Reactive Routing:
   Authenticated:*If a user session exists, it pushes to the `MainNavigationScreen`.
   Unauthenticated:If no user session is detected, it directs the user to the `LoginScreen`.
   Loading State: Displays a `CircularProgressIndicator` while the Firebase stream is initializing.

 3. Identity Verification (`login_screen.dart`)
Credential Handling:Utilizes `TextEditingController` to capture, trim, and validate user email and password inputs.
Error Handling:Features specific exception handling for Firebase errors including `user-not-found`, `wrong-password`, and `invalid-credential` via user-friendly SnackBar feedback.
Security UI: Includes a visibility toggle for the password field and a loading state (`isLoading`) to prevent redundant authentication requests.

4. User Enrollment & Data Sync (`signup_screen.dart`)
Comprehensive Profiles:Captures essential player metadata during registration, including **Name, Position, Skill Level, and Training Goals**.
Cloud Integration:Creates a new user account via **Firebase Auth**.
Simultaneously initializes a structured document in the **Firestore `users` collection** using the user's unique `uid`.
Validation Logic:Includes a front-end check to ensure all fields are filled and that the `password` and `confirmPassword` fields match before processing.

---

Technical Interview Highlights (Viva Lines)

This module controls user access and authentication flow by ensuring a secure, state-driven entry point.”**

State Management:I implemented a reactive approach where the app's navigation state (Logged in vs. Logged out) is driven by a live stream, rather than manual routing logic.
Asynchronous Safety: I utilized `mounted` checks before calling `setState` to prevent memory leaks or crashes during asynchronous Firebase operations.
Scalability:** By storing extended user data in Firestore at signup, the application is architected to support personalized user experiences based on the player's position and goals.

---

Tech Stack
Frontend: Flutter (Dart)
Authentication:Firebase Auth
Database:*Google Cloud Firestore
