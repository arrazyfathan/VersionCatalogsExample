#Setup Version Catalogs on Android Project : 

1. Create file named **libs.version.toml** on gradle folder.
    - Create block **[version]**
    - Create block **[libraries]**
    - Create block **[plugins]**

2. Specify all the dependencies and plugins to **libs.versions.toml**
   
   ##For Default Dependencies
   - build.gradle.kts ( app-module )
      ```
     implementation("androidx.activity:activity-compose:1.8.2")
     ```
   - libs.version.toml
      ```
     [versions]
     activity-compose = "1.8.2"
     
     androidx-activity-compose = { module = "androidx.activity:activity-compose", version.ref = "activity-compose" }
     ```
   
   - replace with this code on build.gradle.kts ( app-module )
      ```
     implementation(libs.androidx.activity.compose)
     ```
   
3. Done