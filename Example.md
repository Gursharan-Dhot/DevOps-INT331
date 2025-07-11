# Maven Tutorial - Minimal Java Application

## What is Maven?
Maven is a build automation and project management tool for Java projects. It handles:
- **Dependencies**: External libraries your project needs
- **Build lifecycle**: Compiling, testing, packaging your code
- **Project structure**: Standard directory layout
- **Artifacts**: The final outputs (JAR files, etc.)

## Project Structure
Create this exact folder structure:

```
my-maven-app/
├── pom.xml
└── src/
    ├── main/
    │   └── java/
    │       └── com/
    │           └── example/
    │               └── App.java
    └── test/
        └── java/
            └── com/
                └── example/
                    └── AppTest.java
```

## File Contents

### 1. pom.xml (Project Object Model)
This is Maven's configuration file - the heart of any Maven project.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    
    <modelVersion>4.0.0</modelVersion>
    
    <!-- Project coordinates (GAV) -->
    <groupId>com.example</groupId>
    <artifactId>my-maven-app</artifactId>
    <version>1.0.0</version>
    <packaging>jar</packaging>
    
    <!-- Project information -->
    <name>My Maven App</name>
    <description>A simple Maven project for learning</description>
    
    <!-- Java version -->
    <properties>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    
    <!-- Dependencies -->
    <dependencies>
        <!-- JUnit for testing -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
    
    <!-- Build configuration -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>11</source>
                    <target>11</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
    
</project>
```

### 2. src/main/java/com/example/App.java
The main application class.

```java
package com.example;

/**
 * Hello world application
 */
public class App {
    
    public static void main(String[] args) {
        System.out.println("Hello World from Maven!");
        
        App app = new App();
        String greeting = app.getGreeting("Maven");
        System.out.println(greeting);
    }
    
    public String getGreeting(String name) {
        return "Hello, " + name + "! Welcome to build automation.";
    }
}
```

### 3. src/test/java/com/example/AppTest.java
Unit test for the application.

```java
package com.example;

import org.junit.Test;
import static org.junit.Assert.*;

/**
 * Unit test for App class
 */
public class AppTest {
    
    @Test
    public void testGetGreeting() {
        App app = new App();
        String result = app.getGreeting("World");
        assertEquals("Hello, World! Welcome to build automation.", result);
    }
    
    @Test
    public void testGetGreetingWithMaven() {
        App app = new App();
        String result = app.getGreeting("Maven");
        assertEquals("Hello, Maven! Welcome to build automation.", result);
    }
}
```

## Setup Instructions for Windows 10

### Prerequisites
1. **Install Java JDK 11 or higher**
   - Download from [Oracle](https://www.oracle.com/java/technologies/downloads/) or [OpenJDK](https://adoptium.net/)
   - Verify installation: `java -version` in Command Prompt

2. **Install Maven**
   - Download from [Maven website](https://maven.apache.org/download.cgi)
   - Extract to `C:\apache-maven-3.x.x`
   - Add to PATH: `C:\apache-maven-3.x.x\bin`
   - Verify installation: `mvn -version` in Command Prompt

### Step 1: Create the Project Structure
**Option A: Using Command Prompt**
```cmd
REM Create the main directory
mkdir my-maven-app
cd my-maven-app

REM Create the directory structure
mkdir src\main\java\com\example
mkdir src\test\java\com\example

REM Create empty files
type nul > pom.xml
type nul > src\main\java\com\example\App.java
type nul > src\test\java\com\example\AppTest.java
```

**Option B: Using File Explorer**
1. Create folder `my-maven-app` on your desktop
2. Inside it, create the folder structure:
   ```
   my-maven-app\
   ├── src\
   │   ├── main\
   │   │   └── java\
   │   │       └── com\
   │   │           └── example\
   │   └── test\
   │       └── java\
   │           └── com\
   │               └── example\
   ```
3. Right-click in each folder and create "New Text Document"
4. Rename the files to:
   - `pom.xml` (in root)
   - `App.java` (in src\main\java\com\example)
   - `AppTest.java` (in src\test\java\com\example)

### Step 2: Copy the file contents
Open each file with Notepad or your preferred text editor and copy the content provided above.

## Essential Maven Commands

### 1. Validate the project
```bash
mvn validate
```
**What it does**: Checks if the project structure and pom.xml are valid.

### 2. Compile the code
```bash
mvn compile
```
**What it does**: 
- Downloads dependencies (JUnit)
- Compiles Java source code
- Creates `target/classes` directory

### 3. Run tests
```bash
mvn test
```
**What it does**:
- Compiles test code
- Runs unit tests
- Creates test reports in `target/surefire-reports`

### 4. Package the application
```bash
mvn package
```
**What it does**:
- Runs compile and test
- Creates JAR file in `target/` directory
- JAR name: `my-maven-app-1.0.0.jar`

### 5. Run the application
```cmd
REM After packaging, run the JAR
java -cp target\my-maven-app-1.0.0.jar com.example.App
```

### 6. Clean the project
```bash
mvn clean
```
**What it does**: Removes the `target` directory and all compiled files.

### 7. Full build cycle
```cmd
mvn clean compile test package
```
**What it does**: Complete build from scratch.

## Key Maven Concepts Explained

### 1. **POM (Project Object Model)**
- `pom.xml` is the core of every Maven project
- Contains project information, dependencies, and build configuration
- Uses XML format

### 2. **GAV Coordinates**
- **GroupId**: Usually your organization's domain (com.example)
- **ArtifactId**: Project name (my-maven-app)
- **Version**: Project version (1.0.0)

### 3. **Standard Directory Layout**
- `src/main/java`: Production Java code
- `src/test/java`: Test code
- `target/`: Generated files (compiled classes, JARs, etc.)

### 4. **Dependencies**
- External libraries your project uses
- Maven downloads them automatically
- Stored in local repository (`~/.m2/repository`)

### 5. **Build Lifecycle**
Maven has three built-in lifecycles:
- **Default**: compile → test → package → install → deploy
- **Clean**: clean
- **Site**: site documentation

### 6. **Scopes**
- `compile`: Available in all classpaths (default)
- `test`: Only available during testing
- `provided`: Available during compile but not runtime

## Windows-Specific Tips

### Using Command Prompt
1. **Open Command Prompt**: Press `Win + R`, type `cmd`, press Enter
2. **Navigate to your project**: `cd C:\path\to\your\my-maven-app`
3. **Run Maven commands**: All the `mvn` commands work the same way

### Using PowerShell (Alternative)
1. **Open PowerShell**: Press `Win + X`, select "Windows PowerShell"
2. **Navigate to project**: `cd C:\path\to\your\my-maven-app`
3. **Run Maven commands**: Same `mvn` commands work

### File Paths
- Maven creates files in `target\` directory (backslashes on Windows)
- Local Maven repository: `C:\Users\YourUsername\.m2\repository`
- Use backslashes `\` in Windows paths instead of forward slashes `/`

### Text Editors
- **Notepad**: Basic but works for this tutorial
- **Notepad++**: Free, better for coding
- **VS Code**: Excellent free editor with Java support
- **IntelliJ IDEA**: Professional IDE with excellent Maven support

### Common Windows Issues
1. **"mvn is not recognized"**: Maven not in PATH
   - Solution: Add Maven's bin directory to your PATH environment variable
2. **"JAVA_HOME not set"**: Java environment variable missing
   - Solution: Set JAVA_HOME to your JDK installation directory
3. **Permission issues**: Run Command Prompt as Administrator if needed

When you run the commands, you'll see:

1. **First run**: Maven downloads dependencies and plugins
2. **Compilation**: Creates `.class` files in `target/classes`
3. **Testing**: Runs tests and shows results
4. **Packaging**: Creates JAR file in `target/`
5. **Execution**: Your "Hello World" program runs

## Next Steps for Learning

1. **Add more dependencies**: Try adding Apache Commons or other libraries
2. **Create more classes**: Add additional Java classes and tests
3. **Explore plugins**: Add plugins for code coverage, documentation
4. **Learn profiles**: Configure different environments (dev, test, prod)
5. **Multi-module projects**: Create projects with multiple modules

This basic setup demonstrates Maven's core concepts and gives you a foundation to build upon!
