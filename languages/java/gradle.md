# Gradle

## Basics

### Core Concepts

- Gradle uses build scripts to automate the building, testing, and deployment of software.
- **Project**: Your software that you want to build.
- **Build Script**: Your instructions telling Gradle how to build your project.
- **Tasks**: A basic unit of work, such as compiling code, or running a test.
- **Plugins**: They add new stuff to Gradle and give you new tasks you can do.

### Gradle Project Structure

```text
project
├── gradle                              
│   ├── libs.versions.toml              
│   └── wrapper
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew                             
├── gradlew.bat                         
├── settings.gradle(.kts)               
├── subproject-a
│   ├── build.gradle(.kts)              
│   └── src                             
└── subproject-b
    ├── build.gradle(.kts)              
    └── src       
```

- `gradle` - Stores wrapper files and more.
- `libs.versions.toml` - Version catalog for dependency management.
- `gradlew` - Gradle wrapper scripts.
- `settings.gradle` - Settings file.
- `build.gradle` - Build scripts.
- `src` - Source code of the project.

## Gradle Wrapper Basics

- The Wrapper is a script that calls the current version of Gradle that you have, and you should use this to do all your Gradle stuff.

    ```bash
    ./gradlew build
    ```

## CLI Basics

- We use the command line interface (CLI) to interact with Gradle. Here is the basic syntax:

    ```bash
    ./gradlew taskName --option-name
    ```

## Settings File Basics

- The settings file lets you add sub-projects to your build. So for single-project builds, your settings file is optional.
- Written in Groovy or Kotlin.

    `settings.gradle.kts`

    ```kotlin
    rootProject.name = "root-project"   

    include("sub-project-a")            
    include("sub-project-b")
    include("sub-project-c")
    ```

## Build File Basics

- A build script details build configuration, tasks, and plugins.
- Every Gradle build must have at least one build script.
- In it, two types of dependencies are specified:
  - Gradle libraries/plugins.
  - The libraries which your source code needs.

### Build Scripts

- The build script is either written in Groovy or Kotlin

    `build.gradle.kts`

    ```kotlin
    plugins {
        id("application")
    }

    application {
        mainClass = "com.example.Main"
    }
    ```

- The `application` plugin facilitates creating an executable JVM application and also implicitly applies the `java` plugin.
