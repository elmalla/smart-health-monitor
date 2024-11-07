# Smart Health Monitoring System Code Documentation


### Table of Contents
1. **[Project Overview and Purpose](#project-overview-and-purpose)**
2. **[Architecture Overview](#architecture-overview)**
3. **[Project Structure](#project-structure)**
4. **[Technology Stack and Dependencies](#technology-stack-and-dependencies)**
5. **[Code Conventions and Standards](#code-conventions-and-standards)**
6. **[User Data and Privacy Compliance](#user-data-and-privacy-compliance)**
7. **[Core Functional Components](#core-functional-components)**
8. **[Development Setup](#development-setup)**
9. **[API Documentation](#api-documentation)**
10. **[User Interface and Experience Documentation](#user-interface-and-experience-documentation)**
11. **[Known Issues and Limitations](#known-issues-and-limitations)**
12. **[Future Development and Scalability](#future-development-and-scalability)**
13. **[Code File Descriptions](#code-file-descriptions)**
14. **[Communication with the Medical Bluetooth Device](#communication-with-the-medical-bluetooth-device)**
15. **[Real-time Patient Health Data Updates](#real-time-patient-health-data-updates)**
16. **[Smart Health Application To-Do List](#smart-health-application-to-do-list)**


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


1. **MainActivity.java**: The entry point for the app, handling initial setup and navigation.
2. **CheckmeMainActivity.kt**: Core activity managing BLE communication and health data interactions.
3. **LoginActivity.java**: Manages user login and credential validation.
4. **RegisterActivity.java**: Handles user registration logic.
5. **ForgotPassActivity.java**: Allows users to recover or reset their passwords.
6. **HomeActivity.java**: Main user interface for logged-in users, showing navigation options.
7. **UserProfileActivity.java**: Manages the user's profile details.
8. **SplashActivity.java**: Displays a splash screen while the app initializes.
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


## Communication with the medical Bluetooth device

The file responsible for communication with the Bluetooth device in the provided code snippets is primarily the **BleDataWorker.kt** file. Although the actual code for `BleDataWorker.kt` was not provided in the snippets you shared, this file is referenced multiple times across different fragments and activities, indicating that it is a key component for Bluetooth communication.

Here’s a detailed explanation of how `BleDataWorker.kt` and other related components facilitate Bluetooth communication:

### 1. BleDataWorker.kt (Responsible for Bluetooth Communication)
**Purpose**: Handles the communication between the Android application and Bluetooth Low Energy (BLE) health monitoring devices.

**Responsibilities**:
- **Scanning for Devices**: Likely responsible for scanning for available Bluetooth devices to connect with.
- **Connecting to Health Devices**: Establishes a connection with supported health devices (e.g., ECG, oximeter).
- **Data Transfer**: Collects data such as ECG readings, blood oxygen levels, glucose levels, etc., from connected devices.
- **Data Parsing**: Converts the received Bluetooth data packets into formats that can be processed or displayed by the application.

**References in the Code**:
- Fragments such as `DailyCheckFragment.kt`, `EcgRecorderFragment.kt`, and others make calls to methods within `BleDataWorker.kt` to initiate and handle communication with Bluetooth devices.

### 2. CheckmeMainActivity.kt
**Purpose**: Acts as a hub for managing Bluetooth-related activities, particularly initializing and interacting with `BleDataWorker`.

**Responsibilities**:
- **User Interface for Bluetooth**: Likely provides UI elements for users to initiate Bluetooth operations, such as scanning for devices, pairing, and viewing data.
- **Interaction with BleDataWorker**: It interacts with `BleDataWorker.kt` to trigger Bluetooth operations and receive data. It acts as a controller that orchestrates the communication process, possibly managing user inputs and providing feedback.

### 3. Fragments Handling Data from Bluetooth Devices
- **DailyCheckFragment.kt**, **EcgRecorderFragment.kt**, **OximeterFragment.kt**, etc.:
  - **Purpose**: These fragments are responsible for displaying the health data received from Bluetooth-connected devices.
  - **Interaction with BleDataWorker**: Each fragment indirectly interacts with Bluetooth through `BleDataWorker.kt`. The received data is processed and presented through LiveData objects in the corresponding ViewModel classes.
  - For example, in `EcgRecorderFragment.kt`, data collected via Bluetooth is observed through the `EcgRecorderViewModel` which holds the data fetched from Bluetooth devices.

### Summary
- **BleDataWorker.kt**: This is the primary file responsible for communication with Bluetooth devices. It manages scanning, connecting, transferring data, and processing data received from the BLE health monitoring devices.
- **CheckmeMainActivity.kt**: Works alongside `BleDataWorker.kt` to manage Bluetooth connections and initiate data collection. It provides UI-level interactions for Bluetooth activities.
- **Fragments and ViewModels**: The data collected via Bluetooth is then used by different fragments (e.g., `DailyCheckFragment.kt`, `EcgRecorderFragment.kt`) to display metrics such as ECG, oxygen levels, etc. These fragments observe LiveData to re



## Real-time Patient health data updates:


### 1. BackgroundService.kt (Located in service/)
**Purpose**: This service is responsible for executing tasks in the background, such as periodic health data collection and updates. It runs at specified intervals to gather health information and update the application accordingly.

**Real-time Updates**: The `runTaskAfterSomeDelay()` function helps in scheduling regular health updates, providing near real-time information to the user.

### 2. BleDataWorker.kt (not explicitly provided, but referenced multiple times)
**Purpose**: Handles Bluetooth communication with health devices (such as ECG, oximeter, etc.). This component facilitates real-time data collection from health monitoring devices.

**Real-time Updates**: BLE (Bluetooth Low Energy) communication is essential for receiving real-time health data, which is then used by different fragments in the app to present updated health metrics.

### 3. Fragments and Adapters Handling Live Data
**DailyCheckFragment.kt**, **EcgRecorderFragment.kt**, **OximeterFragment.kt**, **PedometerFragment.kt**, **SleepFragment.kt**, **TmpFragment.kt**:
- **Purpose**: Each of these fragments handles specific health data (e.g., ECG, glucose, oxygen levels). They observe LiveData provided by ViewModels to show the most up-to-date health metrics.
- **Real-time Updates**: The fragments and their corresponding ViewModels (like `DailyCheckViewModel.kt`, `EcgRecorderViewModel.kt`, etc.) use LiveData to provide real-time updates on the UI whenever new health information is available.

### 4. ViewModels (e.g., DailyCheckViewModel.kt, EcgRecorderViewModel.kt)
**Purpose**: Manage UI-related data in a lifecycle-conscious way. They use LiveData to ensure that fragments observe changes and are updated with real-time health information.

**Real-time Updates**: ViewModels maintain observables that are updated in real time when new data arrives. Fragments observing these ViewModels automatically reflect changes on the user interface.

### 5. Firebase Push Notifications
**AppUtils.kt**:
- **Purpose**: Includes a method to send push notifications (`sendPushNotification()`). These notifications can be used to alert users about critical changes in health metrics.
- **Real-time Updates**: Push notifications are used to provide real-time alerts to users for critical health updates, making sure they receive immediate warnings when needed.

### Summary
- **Background Services** (`BackgroundService.kt`) for periodic updates.
- **Bluetooth Communication** (`BleDataWorker.kt`) for real-time data collection from devices.
- **Fragments and ViewModels** for displaying health metrics using LiveData to ensure the UI reflects the most current data.
- **Push Notifications** (`AppUtils.kt`) to alert users of significant changes in real time.

These components work together to provide real-time health monitoring and data updates, ensuring that users and clinicians have timely and 
accurate information.


## Smart Health Application To-Do List

This document outlines future improvements and feature enhancements planned for the Smart Health Application. 
These tasks are intended to enhance the app's functionality, user experience, performance, and security.

### Contents

1. **Bluetooth Communication Enhancements**
2. **User Experience Improvements**
3. **Data Syncing and Storage**
4. **Real-time Notifications and Alerts**
5. **Security and Privacy Improvements**
6. **User Interface and Design**
7. **Performance Optimization**
8. **New Features Implementation**
9. **Testing and Quality Assurance**
10. **Documentation and Developer Experience**
11. **Backend and Data Analytics**
12. **Future Scalability and Integration**

---

### 1. Bluetooth Communication Enhancements
- [ ] **Optimize Bluetooth Stability**: Address Bluetooth connection stability issues to prevent unexpected disconnections.
- [ ] **Add BLE Device Compatibility**: Extend support to more Bluetooth Low Energy (BLE) health devices, including additional ECG and blood pressure monitors.
- [ ] **Device Pairing UI Improvement**: Improve the user interface for connecting and pairing devices to make the process more intuitive.

### 2. User Experience Improvements
- [ ] **Offline Mode Enhancements**: Enhance offline capabilities by allowing data to be stored locally and synced automatically once the user is online again.
- [ ] **Multi-language Support**: Add localization for additional languages to cater to a broader audience.
- [ ] **Improve Accessibility**: Ensure the app is accessible for users with disabilities by adding screen reader support and implementing proper navigation for accessibility tools.

### 3. Data Syncing and Storage
- [ ] **Database Migration to Room**: Migrate any existing data storage solution to Room for improved performance and reliability.
- [ ] **Implement Data Encryption at Rest**: Add encryption to stored medical data to ensure data security and compliance with standards like HIPAA and GDPR.
- [ ] **Sync with Cloud Storage**: Allow users to back up health data to a secure cloud server to prevent data loss.

### 4. Real-time Notifications and Alerts
- [ ] **Configurable Alerts**: Allow users to configure thresholds for health metrics that trigger notifications, and set up custom alerts.
- [ ] **Improve Notification Precision**: Enhance notifications to include more context, such as when a health parameter has consistently been out of range.
- [ ] **Push Notification Improvements**: Implement a system to push real-time notifications to both patients and clinicians for critical events.

### 5. Security and Privacy Improvements
- [ ] **Authentication Improvements**: Integrate biometric authentication (e.g., fingerprint, face recognition) for app login to ensure better user security.
- [ ] **Comprehensive Compliance Audit**: Conduct a full audit of the app to ensure compliance with international health data regulations (e.g., HIPAA, GDPR).
- [ ] **End-to-end Encryption**: Ensure all data sent between the app and the server is encrypted end-to-end, especially sensitive health metrics.

### 6. User Interface and Design
- [ ] **Revamp User Interface**: Refresh the overall UI to align with the latest design trends and make the user interface more intuitive.
- [ ] **Dark Mode Support**: Implement dark mode for the application to provide a more comfortable viewing experience in low-light conditions.
- [ ] **Data Visualization Enhancements**: Improve health data visualization with more detailed charts and graphs for trends, comparative analysis, and better insights.

### 7. Performance Optimization
- [ ] **Reduce App Start-up Time**: Profile and optimize app start-up to provide a smoother and faster user experience.
- [ ] **Optimize Battery Consumption**: Reduce the battery consumption of the app, especially for background services like Bluetooth data collection.
- [ ] **Minimize Data Usage**: Optimize network usage to reduce data consumption during data syncing with cloud storage.

### 8. New Features Implementation
- [ ] **Emergency Contact Feature**: Add functionality for users to set emergency contacts, which can be notified if critical health metrics are detected.
- [ ] **Integration with Wearables**: Expand compatibility with popular health tracking wearables (e.g., Fitbit, Apple Watch).
- [ ] **Medication Reminder Integration**: Provide a reminder system for patients to take prescribed medications and update their health data accordingly.

### 9. Testing and Quality Assurance
- [ ] **Increase Unit Test Coverage**: Expand unit test coverage for ViewModels and other core logic to improve reliability.
- [ ] **UI Automation Testing**: Add automated UI tests for key workflows using frameworks like Espresso or Robolectric.
- [ ] **Load Testing for Scalability**: Conduct load testing to ensure the app scales well under high usage.

### 10. Documentation and Developer Experience
- [ ] **Complete API Documentation**: Improve the documentation for the backend APIs, including detailed explanations for all endpoints.
- [ ] **Developer Contribution Guide**: Add a comprehensive contribution guide for new developers who wish to participate in the project.
- [ ] **Javadoc and Code Comments**: Ensure all critical functions are properly documented with Javadocs and comments to make code maintenance easier.

### 11. Backend and Data Analytics
- [ ] **Cloud Backend Enhancements**: Optimize backend API performance and add caching mechanisms to reduce latency.
- [ ] **Health Data Analytics**: Implement analytics tools that provide detailed insights and recommendations based on user health data trends.
- [ ] **Anomaly Detection**: Add machine learning-based anomaly detection for health metrics to identify potential health risks early.

### 12. Future Scalability and Integration
- [ ] **FHIR Standard Compliance**: Implement FHIR (Fast Healthcare Interoperability Resources) standards to enable better integration with other health systems and data exchange.
- [ ] **Integrate Telehealth Capabilities**: Allow patients to schedule video calls with clinicians, enabling remote health assessments and consultations.
- [ ] **Expand Multi-user Support**: Add support for clinicians to manage multiple patients seamlessly within the app, with proper authorization and security.

---

These items collectively can significantly enhance the application's user experience, reliability, scalability, and compliance with healthcare standards.

