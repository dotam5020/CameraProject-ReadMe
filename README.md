# CameraProject-ReadMe
## Dependencies <br>
Library are managed using Cocoapods. To include the necessary modules in your project, follow the instructions below:
- Add the module as a dependency to your project using **CocoaPods** or **Swift Package Manager**
- Import the module into your project.
1. **Alamofire**: is an open-source networking library that simplifies the process of sending HTTP requests and handling responses.
   - [Alamofire GitHub](https://github.com/Alamofire/Alamofire.git)
   - Add it to your Podfile:
     ```bash
      pod 'Alamofire'
     ```
2. **SnapKit**: basically adds syntactic sugar over the native auto layout code, which makes understanding and writing auto layout code easier.
   - [SnapKit GitHub](https://github.com/SnapKit/SnapKit.git)
   - Add it to your Podfile:
     ```bash
      pod 'Snapkit'
     ```
3. **Firebase**: is primarily used for user authentication, managing databases (such as Realtime Database and Cloud Firestore) to store and sync real-time data, managing file storage with Firebase Storage, sending push notifications through Cloud Messaging, and integrating analytics tools with Firebase Analytics to track and improve user experience.
   - [Firebase Setup Guide](https://firebase.google.com/docs/ios/setup)
   - Add it to your Podfile:
     ```bash
      pod 'Firebase'
      pod 'Firebase/Core'
     ```
4. **Kingfisher**: is a powerful, pure-Swift library for downloading and caching images from the web. It provides you a chance to use a pure-Swift way to work with remote images in your next app.
   - [Kingfisher GitHub](https://github.com/onevcat/Kingfisher.git)
   - Add it to your Podfile:
     ```bash
      pod 'Kingfisher'
     ```
## Structure and Architecture
- FlowChar
  
  ![url drawio](https://github.com/user-attachments/assets/93295d45-5405-4efc-9c0b-4db05afa3ca1)
  > Diagram of the project's operating mechanism.

- Each Module has its own directory
    - Network
      - ApiRequestManager: used to send network requests (GET/POST/DELETE) from `SourceManager` to the API
      - SourceManager: sends network requests through `ApiRequestManager`, receives responses from the API, and processes them (success or failure)
    - Service
      - Sends request parameters to `Network` and receives JSON data
      - Returns JSON data to `Repository`
    - Repository: manages data from various sources (stored locally or on a server)
      - Local: receives and updates data for `DataSource`
      - Remote: receives JSON data from `Service` and sends data to `Service` from `UseCase`
    - UseCase: transforms data received from `Repository` (Models) into appropriate data (DataMapper) for display on the `View` through ViewModel. It is also where user changes are handled (update data)
    - ViewModel
      - Accesses and updates data from `UseCase` for display on the `View`
      - Receives and processes events from the `View` and updates data for the `View`
    - View
      - Displays data received from `ViewModel` and interacts with the user
      - Sends events to `ViewModel` when the user interacts
    - DataSource: database used to store data locally
    - Models: models typically represent data objects in the application <br>
      **Ex:**<br>
      - used to structure data (JSON, etc) for API requests and responses<br>
      - could be a DataMapper that contains data to be displayed on the View.
    
## Design Pattern
- **Signleton**:
  - Ensures a class has only one instance throughout the app.
  - Provides a single access point for functionality and is initialized only on first use.
  
## Database
- **CoreData**: An object-oriented framework for managing and persisting data within the app.
- **UseDefautl**: A key-value store for simple data types like strings, numbers, and booleans, useful for saving and retrieving lightweight data.
- **Key_Chain**: A secure storage solution for secret values like API keys and passwords, also allowing data sharing between apps.

## Environment Setup
### Prerequisites
- **Xcode**: Version 14.x or higher
- **Swift**: Version 5.x
- **CocoaPods**: Version 1.10.0 or higher

### Tools
- **Xcode**: Primary IDE for IOS development.
- **Swiftline**: Ensures coding standards and linting.
- **Fastlane**: Automates builds and deployments.

## Configuration
### Firebase Setup
1. Download the `GoogleService-Info.plist` from the Firebase Console.
2. Add it to your Xcode project.
3. Initialize Firebase in your AppDelegate or SceneDelegate.

### API Endpionts
- **Development**: `https://api-dev.ex.com`
- **Production**: `https://api.ex.com`

### Environment Variables
Set environment-specific variables in the `Info.plist` or use a configuration management tool.

## Installation and Setup
### Step 1: Clone the Repository <br>
Clone the project from the repository:
```bash
git clone https://github.com/dotam5020/CameraProject-ReadMe.git
cd CameraProject-ReadMe
```
### Step 2: Install Dependencies <br>
Install project dependencies using CocoaPods:
```bash
pod install
```
### Step 3: Open th Project <br>
Open the project using the `.xcworkspace` file:
```bash
open CameraProject-ReadMe.xcworkspace
```
### Step 4: Build and Run <br>
Select the target device or simulator and run the project:
- Use `Cmd + R` to build and run the app.

## Respectful Usage of Xcode and Swift
- **Adhere to Best Practices**: Ensure code quality and modularity.
- **Fllow Established Coventions**: Maintain consistency across the codebase.
- **Frequent Commits**: Use meaningful commit messages and follow the branching strategy.

## Additional Resources:
- [Swift Documentation](https://developer.apple.com/documentation/swift/)
- [Xcode User Guide](https://developer.apple.com/documentation/xcode)
- [Firebase Setup Guide](https://firebase.google.com/docs/ios/setup)





