# Smart Health Monitoring System Code Documentation

## Project Overview and Purpose

The Smart Health Monitoring System is an Android application designed to help users monitor various health metrics in real time. 
It includes features for tracking heart rate, ECG, oxygen levels, glucose, pedometer, and sleep data. The intended users are patients, 
doctors, and guardians, allowing for effective health tracking, remote monitoring, and health data sharing.

### Objectives:
The app aims to assist users in monitoring critical health metrics, thus providing early warning signs for medical 
conditions and enabling data-driven discussions between patients and healthcare providers.

### Core Features:
- **Real-time Health Monitoring**: Tracks heart rate, ECG, glucose levels, oxygen levels, temperature, and steps in real time.
- **Data Visualization**: Presents collected health metrics in an easy-to-understand format.
- **Notifications and Alerts**: Provides reminders for medication and alerts for abnormal health metrics.
- **User Profiles**: Manages user data including patient history and profile information.

## Architecture Overview

### Architecture Pattern:
The application uses the **Model-View-ViewModel (MVVM)** architecture pattern. This separation of concerns enhances testability, modularity, and maintainability, ensuring a clear 
distinction between UI-related logic and business data.

### Component Diagram:
The application consists of multiple fragments for individual health metrics, activities for user interaction, view models 
for managing UI data, and services for background tasks. The MVVM pattern keeps UI components in sync with live data from the backend.

### Data Flow:
1. **User Input**: Users interact via UI components (e.g., entering data, pressing buttons).
2. **ViewModel**: Data is processed or fetched by ViewModels, providing a clear interface to the fragments.
3. **Backend Services**: Interactions like BLE data transfers are managed by services, with data either stored locally or sent to the cloud.
4. **UI Update**: UI is updated by observing LiveData objects held in ViewModels.

## Project Structure

### Folder Structure Explanation:
- **ui/**: Contains all UI components, including fragments and activities.
- **viewmodel/**: Holds ViewModel classes, responsible for managing and storing UI-related data.
- **adapter/**: RecyclerView adapters for various lists (e.g., daily health data, ECG records).
- **service/**: Contains services such as the `BackgroundService.kt` for managing background tasks.
- **network/**: API client and interface for interacting with remote servers using Retrofit.
- **utils/**: Utility classes for general helper functions used across the application.
- **data/**: Models representing different health metrics, such as `EcgWaveInfo`, `GluBean`, etc.

### Important Files:
- **MainActivity.kt**: Entry point of the app, sets up navigation to various features.
- **CheckmeMainActivity.kt**: Manages core functionalities related to BLE communication and health metrics.
- **ApiClient.kt**: Configures Retrofit to interact with remote APIs.
- **AppUtils.kt**: Contains utility methods like date formatting, sending notifications, etc.

## Technology Stack and Dependencies

### Android SDK and Minimum API Level:
- **SDK Version**: Android SDK 29 and above.
- **Minimum API Level**: API Level 21 (Lollipop).

### Third-party Libraries:
- **Retrofit**: For network requests and communication with APIs.
- **OkHttp**: For enhanced logging and request/response interception.
- **Gson**: To convert Java objects into JSON and vice versa.
- **Firebase**: For notifications and cloud storage.

### Custom Libraries or Frameworks:
- Custom Bluetooth communication and BLE data handling implemented within `BleDataWorker.kt`.

## Code Conventions and Standards

### Coding Style Guide:
- **Naming Conventions**: Classes are named in PascalCase, variables and methods in camelCase.
- **Spacing and Indentation**: Consistent use of 4-space indentation.

### UI/UX Standards:
- Consistent use of colors and typography for accessibility.
- All primary actions are highlighted in blue, with a clear call to action.

### Error Handling and Logging:
- Uses **Timber** for logging, with different levels (`d` for debug, `e` for errors).
- Critical errors are caught using `try/catch` blocks, with user-friendly messages displayed via `Toast`.

## User Data and Privacy Compliance

### Data Protection Practices:
- User data is handled using encrypted storage and transferred via secure channels.

### Encryption & Security:
- **AES Encryption**: Applied to locally stored medical data.
- **HTTPS**: All API communications are done over secure HTTPS connections.

### Compliance Requirements:
- Adheres to GDPR guidelines for data protection and privacy.
- Data policies ensure compliance with HIPAA for health information where applicable.

## Core Functional Components

### Medical Data Processing:
- Handles data collected from BLE health devices, processes it, and stores it securely.
- **DailyCheckFragment.kt** and `DailyCheckViewModel.kt` process daily health data for display and analysis.

### Networking & API Services:
- Uses **Retrofit** for API calls to handle user authentication and notification services.
- **Firebase** is used for push notifications.

### Database Structure:
- **SharedPreferences**: Stores simple key-value pairs for app settings.
- **Custom File System Storage**: Uses `.dat` files to store various health metrics, accessed using helper classes like `ReadCheckmeFilesHelper.kt`.

### Notification System:
- Notifications are handled using Firebase, with logic encapsulated in `AppUtils.kt`.

### Data Syncing & Offline Mode:
- Data is periodically synced when a network connection is available, and stored locally during offline periods.

## Development Setup

### Installation Requirements:
- **Tools**: Android Studio (latest version), Java 8 or Kotlin.
- **Gradle**: Version 5.4.1 or higher.

### Configuration and Environment Variables:
- **API Keys**: Stored in local property files (`local.properties`) to prevent exposure.

### Build Instructions:
- Run `./gradlew build` to build the project.
- Use Android Studio to run and debug on an emulator or physical device.

## API Documentation

### Endpoints and Parameters:
- **Login**: `/api/login` (POST) – Expects email and password.
- **Push Notifications**: `/send` (POST) – Sends notification data.

### Authentication Details:
- Uses token-based authentication for secure access to APIs.

### Error Codes and Messages:
- **401 Unauthorized**: Invalid credentials during login.
- **500 Server Error**: Issues with the server.

## User Interface and Experience Documentation

### UI Components and Screens:
- **Home Screen**: Displays an overview of all health metrics.
- **Profile Screen**: Allows the user to view/edit profile information.

### UX Workflow:
- Users typically start from the **HomeActivity**, and then navigate to individual metrics like ECG, glucose, or pedometer by selecting options.

### Localization and Accessibility:
- Currently supports **English**; additional languages can be added using the Android localization framework.
- Accessibility support for screen readers and high contrast is implemented for vision-impaired users.

## Known Issues and Limitations

### Unresolved Bugs:
- **ECG Data Occasionally Not Displayed**: Sometimes the ECG wave does not show, potentially due to BLE connectivity issues.

### Feature Limitations:
- **Offline Mode**: Limited functionality when there is no internet connection. Some features require real-time cloud sync.

## Future Development and Scalability

### Roadmap for New Features:
- Integration with more health devices (e.g., smart scales).
- Improved analytics for better health trend visualization.

### Scalability Considerations:
- Plan to implement cloud database storage for larger data sets and remote analysis.


## Code File Descriptions

### Brief Description of Each File

1. **MainActivity.kt**: The entry point for the app, handling initial setup and navigation.
2. **CheckmeMainActivity.kt**: Core activity managing BLE communication and health data interactions.
3. **LoginActivity.kt**: Manages user login and credential validation.
4. **RegisterActivity.kt**: Handles user registration logic.
5. **ForgotPasswordActivity.kt**: Allows users to recover or reset their passwords.
6. **HomeActivity.kt**: Main user interface for logged-in users, showing navigation options.
7. **UserProfileActivity.kt**: Manages the user's profile details.
8. **SplashActivity.kt**: Displays a splash screen while the app initializes.
9. **DailyCheckFragment.kt**: Manages daily health checks and the display of relevant data.
10. **DailyCheckViewModel.kt**: ViewModel for `DailyCheckFragment`, holding and processing daily health data.
11. **DailyViewAdapter.kt**: Adapter to display daily health data in a RecyclerView.
12. **EcgRecorderFragment.kt**: Handles the user interface for recording and displaying ECG data.
13. **EcgRecorderViewModel.kt**: ViewModel for managing ECG recording logic and UI interactions.
14. **EcgViewAdapter.kt**: Adapter for listing recorded ECG entries.
15. **GluFragment.kt**: Displays glucose data for the user.
16. **GluViewAdapter.kt**: Adapter for displaying glucose information.
17. **GluViewModel.kt**: Manages glucose-related data and user interactions.
18. **MyDeviceFragment.kt**: Shows details about connected health devices.
19. **OximeterFragment.kt**: Displays oximeter data, such as oxygen levels and pulse.
20. **OximeterViewModel.kt**: ViewModel for `OximeterFragment`, managing the oximeter data.
21. **OxyViewAdapter.kt**: Adapter for displaying oxygen level data in a list.
22. **PedometerFragment.kt**: Displays step count and related metrics.
23. **PedViewAdapter.kt**: Adapter for listing pedometer data.
24. **PedViewModel.kt**: ViewModel to handle pedometer-related logic and data.
25. **SleepFragment.kt**: Displays sleep metrics, such as sleep duration and quality.
26. **SleepViewAdapter.kt**: Adapter for listing sleep data in a RecyclerView.
27. **SleepViewModel.kt**: Manages the sleep-related data.
28. **TmpFragment.kt**: Displays temperature data for users.
29. **TmpViewAdapter.kt**: Adapter for temperature data.
30. **TmpViewModel.kt**: ViewModel to manage temperature data.
31. **WaveAdapter.kt**: Adapter for visualizing waveform data such as ECG.
32. **WaveView.kt**: Custom view class for rendering waveforms on the screen.
33. **FriendDate.kt**: Data model representing a friend's activity date.
34. **LiveMonitorPostedModel.kt**: Represents live health data posted by the user.
35. **notificationRequest.kt**: Defines the structure for push notification requests.
36. **Requests.kt**: Model for managing user requests within the application.
37. **ApiClient.kt**: Sets up and configures the Retrofit API client.
38. **ApiInterface.kt**: Defines API endpoints for server interaction.
39. **AppIntroActivity.kt**: Manages the app's introductory slides for new users.
40. **PermissionActivity.kt**: Handles requesting and managing permissions.
41. **BackgroundService.kt**: Background service for periodic data updates.
42. **AppUtils.kt**: Utility functions used across the app (e.g., date formatting, notifications).
43. **ByteArray.kt**: Utility functions for handling `ByteArray` operations.
44. **ReadCheckmeFilesHelper.kt**: Helper class for reading health data files.
45. **LeftHead.kt**: ViewModel for managing the left head part of the user interface.
46. **ExampleUnitTest.kt**: Provides unit tests to validate application components.
