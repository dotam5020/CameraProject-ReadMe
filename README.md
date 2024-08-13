# CameraProject-ReadMe
## Dependencies <br>
Library are managed using Cocoapods:
- Add the module as a dependency to your project using **CocoaPods** or **Swift Package Manager**
- Import the module into your project.
1. [Alamofire](https://github.com/Alamofire/Alamofire.git) is an open-source networking library written in Swift that simplifies the process of sending HTTP requests and handling responses. It supports various HTTP methods and includes additional features like parameter encoding and response validation.
```bash
  pod 'Alamofire'
```
2. [SnapKit](https://github.com/SnapKit/SnapKit.git) basically adds syntactic sugar over the native auto layout code, which makes understanding and writing auto layout code easier.
```bash
  pod 'Snapkit'
```
3. [Firebase](https://firebase.google.com/docs/ios/setup) is primarily used for user authentication, managing databases (such as Realtime Database and Cloud Firestore) to store and sync real-time data, managing file storage with Firebase Storage, sending push notifications through Cloud Messaging, and integrating analytics tools with Firebase Analytics to track and improve user experience.
```bash
  pod 'Firebase'
  pod 'Firebase/Core'
```
4. [Kingfisher](https://github.com/onevcat/Kingfisher.git) is a powerful, pure-Swift library for downloading and caching images from the web. It provides you a chance to use a pure-Swift way to work with remote images in your next app.
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
- Signleton:
  - Singleton is a design pattern that ensures a class can have only one object instance throughout the app memory and provide all the code functionality through a single point of access to it.
  - Singleton is initialised only the first time whenever you use it.
  
## Database
- CoreData
  - Core Data is a framework that provides an object-oriented approach to managing and persisting data in your application.
- UseDefautl
  - User Defaults is a key-value store provided by Apple for saving simple data types such as strings, numbers, and booleans. It is an easy-to-use solution for saving and retrieving data without the need for a database
- Key_Chain
  - Keychain is perfect to store secret values (API keys, password, …) with security. It can also be used to share values between projects safely, this is amazing for teams that need to share a password, tokens or whatever they want, from an app to others.
