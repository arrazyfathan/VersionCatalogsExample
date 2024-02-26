# Setup Version Catalogs on Android Project : 

1. Create file named **libs.version.toml** on gradle folder.
    - Create block **[version]**
    - Create block **[libraries]**
    - Create block **[plugins]**

2. Specify all the dependencies and plugins to **libs.versions.toml**
   
   ## For Default Dependencies
   - build.gradle.kts ( app-module )
      ```kotlin
     implementation("androidx.activity:activity-compose:1.8.2")
     ```
   - libs.version.toml
      ```kotlin
     [versions]
     activity-compose = "1.8.2"

     [libraries]
     androidx-activity-compose = { module = "androidx.activity:activity-compose", version.ref = "activity-compose" }
     ```
   
   - replace with this code on build.gradle.kts ( app-module )
      ```kotlin
     implementation(libs.androidx.activity.compose)
     ```

   ## For BOM Dependencies

   	- app module
     ```kotlin
     implementation(platform("androidx.compose:compose-bom:compose-bom:2023.08.00"))
     implementation("androidx.compose.ui:ui")
     ```

	- libs.version.toml
  	```kotlin
    [version]
	compose-bom = "2023.08.00"
      
   	[libraries]
   	androidx-compose-bom = { module = "androidx.compose:compose-bom", version.ref = "compose-bom" }
   	androidx-compose-ui = { group = "androidx.compose.ui", name = "ui" }
	```
  
    - app module
    ```kotlin
    implementation(platform(libs.androidx.compose.bom))
    implementation(libs.androidx.compose.ui)
    ```

	## For Plugins

	- Project module
      ```kotlin
      id("com.android.application") version "8.2.2" apply false
      ```

    - libs.versions.toml
	  ```kotlin
      [version]
      agp = "8.2.2"

      [plugins]
      androidApplication = { id = "com.android.application", version.ref = "agp" }
      ```	

    - Project module
  	  ```kotlin
      alias(libs.plugins.androidApplication) apply false
      ```

   - app module
  
     ```kotlin
     alias(libs.plugins.androidApplication)
     ```
      
3. Done