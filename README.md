## Gradle Install: 

Gradle is a highly scalable build automation tool designed to handle everything from large, multi-project enterprise builds to quick development tasks across various languages. Gradle’s modular, performance-oriented architecture seamlessly integrates with development environments, making it a go-to solution for building, testing, and deploying applications on Java, Kotlin, Scala, Android, Groovy, C++, and Swift.



#### Prerequisites:
- Gradle runs on all major operating systems and requires only a **Java JDK** version 8 or higher to be installed.


_To check Java:_

```
java -version
```





### Download Gradle Binary:

Go to the official Gradle website to download the latest binary distribution: 

- Official Gradle Website: `https://gradle.org/releases/`


Alternatively, you can use `wget` or `curl` to download the latest release directly to your system:

```
cd /opt

wget https://services.gradle.org/distributions/gradle-8.11-bin.zip

wget https://services.gradle.org/distributions/gradle-8.10.2-bin.zip
```


```
unzip gradle-8.10.2-bin.zip

mv gradle-8.10.2 gradle
```


```
ll gradle

drwxr-xr-x   2 root root  38 Feb  1  1980 bin
drwxr-xr-x   2 root root  24 Feb  1  1980 init.d
drwxr-xr-x   4 root root 12K Feb  1  1980 lib
-rw-r--r--   1 root root 24K Feb  1  1980 LICENSE
-rw-r--r--   1 root root 868 Feb  1  1980 NOTICE
-rw-r--r--   1 root root 976 Feb  1  1980 README
```


### Set Up Environment Variables::

```
vim /etc/profile.d/gradle.sh


export GRADLE_HOME=/opt/gradle
export PATH=$GRADLE_HOME/bin:$PATH
```


```
source /etc/profile.d/gradle.sh
```


```
echo $GRADLE_HOME
```


```
gradle -v


Welcome to Gradle 8.10.2!

Here are the highlights of this release:
 - Support for Java 23
 - Faster configuration cache
 - Better configuration cache reports

For more details see https://docs.gradle.org/8.10.2/release-notes.html


------------------------------------------------------------
Gradle 8.10.2
------------------------------------------------------------

Build time:    2024-09-23 21:28:39 UTC
Revision:      415adb9e06a516c44b391edff552fd42139443f7

Kotlin:        1.9.24
Groovy:        3.0.22
Ant:           Apache Ant(TM) version 1.10.14 compiled on August 16 2023
Launcher JVM:  11.0.23 (Red Hat, Inc. 11.0.23+9-LTS)
Daemon JVM:    /usr/lib/jvm/java-11-openjdk-11.0.23.0.9-2.el7_9.x86_64 (no JDK specified, using current Java home)
OS:            Linux 3.10.0-1160.99.1.el7.x86_64 amd64
```


---
---


### Building Java Applications Sample:


```
mkdir demo
cd demo
```


_Initialize a new Gradle project:_

```
gradle init
```


```
### Output:

Starting a Gradle Daemon (subsequent builds will be faster)

Select type of build to generate:
  1: Application
  2: Library
  3: Gradle plugin
  4: Basic (build structure only)
Enter selection (default: Application) [1..4] 1

Select implementation language:
  1: Java
  2: Kotlin
  3: Groovy
  4: Scala
  5: C++
  6: Swift
Enter selection (default: Java) [1..6] 1

Enter target Java version (min: 7, default: 21): 11

Project name (default: demo):

Select application structure:
  1: Single application project
  2: Application and library project
Enter selection (default: Single application project) [1..2] 1

Select build script DSL:
  1: Kotlin
  2: Groovy
Enter selection (default: Kotlin) [1..2]

Select test framework:
  1: JUnit 4
  2: TestNG
  3: Spock
  4: JUnit Jupiter
Enter selection (default: JUnit Jupiter) [1..4]

Generate build using new APIs and behavior (some features may change in the next minor release)? (default: no) [yes, no]


> Task :init
Learn more about Gradle by exploring our Samples at https://docs.gradle.org/8.10.2/samples/sample_building_java_applications.html

Deprecated Gradle features were used in this build, making it incompatible with Gradle 9.0.

You can use '--warning-mode all' to show the individual deprecation warnings and determine if they come from your own scripts or plugins.

For more on this, please refer to https://docs.gradle.org/8.10.2/userguide/command_line_interface.html#sec:command_line_warnings in the Gradle documentation.

BUILD SUCCESSFUL in 2m 22s
1 actionable task: 1 executed

```





Or,


```
gradle init --type java-application
```


```
### Output:

Enter target Java version (min: 7, default: 21): 11

Project name (default: demo):

Select application structure:
  1: Single application project
  2: Application and library project
Enter selection (default: Single application project) [1..2] 1

Select build script DSL:
  1: Kotlin
  2: Groovy
Enter selection (default: Kotlin) [1..2] 1

Select test framework:
  1: JUnit 4
  2: TestNG
  3: Spock
  4: JUnit Jupiter
Enter selection (default: JUnit Jupiter) [1..4]

Generate build using new APIs and behavior (some features may change in the next minor release)? (default: no) [yes, no]


> Task :init
Learn more about Gradle by exploring our Samples at https://docs.gradle.org/8.10.2/samples/sample_building_java_applications.html

Deprecated Gradle features were used in this build, making it incompatible with Gradle 9.0.

You can use '--warning-mode all' to show the individual deprecation warnings and determine if they come from your own scripts or p                        lugins.

For more on this, please refer to https://docs.gradle.org/8.10.2/userguide/command_line_interface.html#sec:command_line_warnings i                        n the Gradle documentation.

BUILD SUCCESSFUL in 23s
1 actionable task: 1 executed
```





```
tree

.
├── app
│   ├── build.gradle.kts
│   └── src
│       ├── main
│       │   ├── java
│       │   │   └── org
│       │   │       └── example
│       │   │           └── App.java
│       │   └── resources
│       └── test
│           ├── java
│           │   └── org
│           │       └── example
│           │           └── AppTest.java
│           └── resources
├── gradle
│   ├── libs.versions.toml
│   └── wrapper
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew
├── gradlew.bat
└── settings.gradle.kts

```



#### Review the project files:

```
cat settings.gradle.kts


/*
 * This file was generated by the Gradle 'init' task.
 *
 * The settings file is used to specify which projects to include in your build.
 * For more detailed information on multi-project builds, please refer to https://docs.gradle.org/8.10.2/userguide/multi_project_builds.html in the Gradle documentation.
 */

plugins {
    // Apply the foojay-resolver plugin to allow automatic download of JDKs
    id("org.gradle.toolchains.foojay-resolver-convention") version "0.8.0"
}

rootProject.name = "demo"
include("app")
```


#### Generated `src/main/java/org/example/App.java`:

```
cat app/src/main/java/org/example/App.java


/*
 * This source file was generated by the Gradle 'init' task
 */
package org.example;

public class App {
    public String getGreeting() {
        return "Hello World!";
    }

    public static void main(String[] args) {
        System.out.println(new App().getGreeting());
    }
}
```




### Build and Run the Application:

_To Build the Application:_

```
./gradlew build
```


_To Run the Application:_

```
./gradlew run
```


You should see the output:

```
> Task :app:run

Hello World!
```



### Gradle General Commands:

- `gradle init` : Initialize a New Project and Creates a new Gradle project with a basic structure.
- `gradle clean` : Deletes the build directory to remove previous build artifacts.
- `gradle build` : Compiles, tests, and packages the code into a distributable format (e.g., .jar file).
- `gradle run` : Run the Application (for projects with the application plugin) and Executes the main class defined in the project.
- `gradle test` : Runs all test cases in the project.
- `gradle tasks` : Displays all available tasks in the project with descriptions.
- `gradle dependencies` : Shows all dependencies used by the project, including transitive dependencies.
- `gradle build --scan` : Produces a detailed build scan report that can be shared for troubleshooting and performance analysis.
- `gradle build --profile` : Generates a profile report for the build to identify any performance bottlenecks.





### Links: 
- [Gradle install](https://gradle.org/install/)
- [Gradle distributions](https://services.gradle.org/distributions/)
- [Gradle Releases](https://gradle.org/releases/)
- [Gradle | Github](https://github.com/gradle/gradle)
- [Gradle User Manual](https://docs.gradle.org/current/userguide/installation.html)
- [Building Java Applications | Docs](https://docs.gradle.org/current/samples/sample_building_java_applications.html)


That’s it! Gradle is now installed and ready for use on your system.

