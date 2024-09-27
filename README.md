# chat_app

A new Flutter project.

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://docs.flutter.dev/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://docs.flutter.dev/cookbook)

For help getting started with Flutter development, view the
[online documentation](https://docs.flutter.dev/), which offers tutorials,
samples, guidance on mobile development, and a full API reference.

AUTHENTICATION SCREEN :-
This code is a **Flutter** implementation for an authentication screen with **Firebase** integration. Here's a breakdown of the architecture:

### 1. **Firebase Integration**
   - The app uses **Firebase Authentication** to handle user sign-in and sign-up.
   - **Firebase Firestore** is used to store user information (email, username, and image URL) in a "users" collection.
   - **Firebase Storage** is used to store user profile images.

### 2. **Stateful Widget: `AuthScreen`**
   - The screen is built using a **stateful widget** (`AuthScreen`) to manage user interaction and state changes.
   - The `_AuthScreen` state class contains:
     - **Form State**: A form with fields for email, username, and password.
     - **Login/Signup Mode**: The screen can toggle between login and sign-up modes using the `_isLogin` boolean.
     - **Image Selection**: A user can select a profile image when signing up, handled by the `_selectedImage` variable and a custom widget `UserImagePicker`.

### 3. **Form Handling**
   - The form uses a `GlobalKey<FormState>` to manage form validation and saving.
   - Fields for email, password, and (for sign-up) username are validated before submission.
   - The `onSaved` callbacks store user input values in state variables (`_enteredEmail`, `_enteredUsername`, `_enteredPassword`).

### 4. **Authentication Logic**
   - When the user submits the form (`_submit` method):
     - The form is validated.
     - If in **Login** mode (`_isLogin` is true), the app calls `signInWithEmailAndPassword()` to authenticate the user.
     - If in **Sign-Up** mode, it calls `createUserWithEmailAndPassword()` to register the user, uploads the selected image to **Firebase Storage**, and saves the user’s details (email, username, and image URL) in **Firestore**.
   - **Error Handling**: If a `FirebaseAuthException` occurs, the error message is displayed using `ScaffoldMessenger`.

### 5. **UI Components**
   - The UI consists of a **Form** within a `Card` that is wrapped by a `SingleChildScrollView` for scrolling.
   - The form includes:
     - A **profile image picker** (only for sign-up).
     - **TextFormFields** for email, username (only in sign-up), and password.
     - **Submit Button**: Depending on the mode (login or sign-up), the button text changes.
     - **Switch Mode Button**: A text button that toggles between login and sign-up.
   - A loading indicator (`CircularProgressIndicator`) is shown while the app is authenticating.

### 6. **Third-Party Libraries**
   - **Firebase Authentication**: Handles user sign-in and sign-up.
   - **Firebase Firestore**: Stores additional user data (username, email, image URL).
   - **Firebase Storage**: Stores profile images.

### **Architecture Flow**
1. **Form Submission**: When the user submits the form, the `_submit` function is triggered.
2. **Authentication**: The app checks if it's a login or sign-up scenario:
   - **Login**: Calls Firebase's `signInWithEmailAndPassword`.
   - **Sign-Up**: Creates a new user, uploads their profile image to Firebase Storage, and stores additional user information in Firestore.
3. **State Management**: The app uses the widget's state to track form fields, image selection, and whether the app is authenticating.
4. **User Feedback**: Displays errors or a success message via `ScaffoldMessenger`, and shows a loading indicator during authentication.

This architecture follows the **MVVM** pattern commonly used in Flutter apps:
- **Model**: Firebase handles the back-end services (auth, storage, database).
- **View**: The `AuthScreen` widget and its form fields build the UI.
- **ViewModel**: State management and business logic are handled in `_AuthScreen`.







CHAT SCREEN :-
This `ChatScreen` widget is a **stateless widget** in a Flutter app designed for a real-time chat application. It integrates with **Firebase Authentication** and utilizes two custom widgets (`ChatMessages` and `NewMessage`) to display messages and send new ones. Here's a breakdown of the architecture:

### 1. **App Structure**
   - The `ChatScreen` widget represents the main chat interface of the app. It has two main components:
     - **App Bar**: Displays the title "FlutterChat" and an action button to sign out.
     - **Body**: Contains a list of chat messages and a form to send new messages.

### 2. **Firebase Integration**
   - **FirebaseAuth**: Used to handle user authentication. The user can sign out by pressing the button in the app bar.
   - `FirebaseAuth.instance.signOut()`: Logs the user out and redirects them to the authentication screen.

### 3. **Widgets Used**
   - **ChatMessages**: A custom widget that likely displays the list of chat messages (using `StreamBuilder` or similar to update messages in real-time).
   - **NewMessage**: Another custom widget that likely contains a form or text input field for sending new messages to the chat.

### 4. **App Bar**
   - The `AppBar` displays the app's title and includes a **sign-out button**:
     - The button triggers the `FirebaseAuth.instance.signOut()` method, which signs the user out of the app.
     - The button's icon is `Icons.exit_to_app`, representing the "log out" functionality.
     - The icon's color is dynamically assigned from the current theme's primary color.

### 5. **Body Layout**
   - The body of the `Scaffold` contains a **column** with two widgets:
     1. **ChatMessages**: This widget occupies most of the space (using `Expanded`) to display the chat messages in a scrollable list.
     2. **NewMessage**: This widget is fixed at the bottom of the screen and likely includes the input for sending new chat messages.

### **Architecture Overview**
- **Stateless Widget**: Since `ChatScreen` does not manage its own state, it's stateless. State changes (e.g., new messages) are likely handled in the `ChatMessages` or `NewMessage` widgets.
- **Separation of Concerns**: The screen is composed of smaller custom widgets (`ChatMessages` and `NewMessage`), following good practices for reusability and readability.
- **Firebase**: Firebase Authentication is used for managing the user's session. This ensures the user can sign out via the action button.

### **Flow of the App**
1. **AppBar**: The user can sign out via the sign-out button in the app bar.
2. **ChatMessages**: Displays chat messages dynamically, likely using Firebase Firestore for real-time updates.
3. **NewMessage**: Provides a way for the user to send new messages to the chat.

This architecture follows the **separation of concerns** principle, where authentication, message display, and message sending are handled independently by different components.








SPLASH SCREEN :-
The `SplashScreen` widget in this code is a **stateless widget** that serves as a basic loading screen for a Flutter app. It typically appears when the app is starting or performing some background initialization (e.g., authentication or data loading). Here's a breakdown of its architecture:

### 1. **Stateless Widget**
   - The `SplashScreen` is a **stateless widget**, meaning it doesn't manage any internal state and its appearance is static. It simply renders the UI.

### 2. **Scaffold Structure**
   - **Scaffold**: The `Scaffold` widget provides the basic material design layout structure (app bar, body, etc.).
   - **AppBar**: The screen includes an app bar at the top with the title "FlutterChat".
   - **Body**: The body contains a `Center` widget, which centers its child widget on the screen.
     - Inside the `Center` is a simple `Text` widget displaying "Loading..." to inform users that the app is in the process of initializing.

### 3. **Architecture Overview**
   - **UI Structure**: This screen consists of an app bar and a centered text widget indicating that something (like data or resources) is being loaded.
   - **Splash Screen Purpose**: Typically, splash screens are used for loading or transition states, and this simple implementation follows that purpose.
   - **No State Management**: As a stateless widget, it doesn’t need to track or manage any state changes. If any dynamic content or transitions were needed, it would either use a `StatefulWidget` or trigger a navigation event after some async operation completes.

### **Flow of the App**
1. **AppBar**: Displays the title of the app ("FlutterChat").
2. **Body**: Displays the "Loading..." text at the center of the screen while the app performs initialization tasks in the background.

The `SplashScreen` acts as a placeholder screen that can be displayed while the app is performing background tasks like fetching data, authenticating users, or preparing the main interface.
