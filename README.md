# CameraProject-ReadMe
##**Dependencies** <br>
Library are managed using Cocoapods:
```bash
  pod 'Alamofire'
  pod 'Snapkit'
  pod 'Firebase'
  pod 'Firebase/Core'
  pod 'Kingfisher'
```
##**Structure and Architecture**
- FlowChar <br><br>
  ![url drawio](https://github.com/user-attachments/assets/93295d45-5405-4efc-9c0b-4db05afa3ca1)

- Each Module has its own directory
    + Network
      * ApiRequestManager: used to send network requests (GET/POST/DELETE) from `SourceManager` to the API
      * SourceManager: sends network requests through `ApiRequestManager`, receives responses from the API, and processes them (success or failure)
    + Service
      * Sends request parameters to `Network` and receives JSON data
      * Returns JSON data to `Repository`
    + Repository: manages data from various sources (stored locally or on a server)
      * Local: receives and updates data for `DataSource`
      * Remote: receives JSON data from `Service` and sends data to `Service` from `UseCase`
    + UseCase: transforms data received from `Repository` (Models) into appropriate data (DataMapper) for display on the `View` through ViewModel. It is also where user changes are handled (update data)
    + ViewModel
      * Accesses and updates data from `UseCase` for display on the `View`
      * Receives and processes events from the `View` and updates data for the `View`
    + View
      * Displays data received from `ViewModel` and interacts with the user
      * Sends events to `ViewModel` when the user interacts
    + DataSource: database used to store data locally
    + Models: models typically represent data objects in the application <br>
      **Ex:**<br>
      * used to structure data (JSON, etc) for API requests and responses<br>
      * could be a DataMapper that contains data to be displayed on the View.
    
##**Design Pattern**
- Signleton

##**Database**
- CoreData
- UseDefautl
- Key_Chain
  
##**Answer the question**
- The use of double-headed arrows aims to indicate that the module both sends and receives data
- Square is used to indicate a layer, and circle represents an important component within that layer (for this project)
- `DataSource` (saves local data) and `SourceManager` (handles API responses)
  + The relationship between local and remote: 2 different data sources
  + Storage: local (on the device) and remote (on the server)
- `ViewModel` and `Models`: Models (Data Mapper) contains data sent from `UseCase` to `ViewModel`, and `ViewModel` updates the Model when it receives changes from the `View` as the User interacts. (In this case, the Model can also be understood as a DataMapper)
