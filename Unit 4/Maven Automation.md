# Maven Build Automation

---

# 1. Introduction to Maven

## What is Maven?

Maven is a Build Automation and Project Management Tool primarily used for Java projects.

It helps developers:

- Compile code
- Run tests
- Manage dependencies
- Package applications
- Deploy applications

Maven follows the principle:

> Convention Over Configuration

Meaning Maven provides a standard project structure and build process, reducing manual configuration.

---

# Why Build Tools Exist?

Before build tools, developers had to manually:

- Compile source code
- Download libraries
- Manage classpaths
- Run tests
- Package applications
- Deploy applications

This was time-consuming and error-prone.

Build tools automate these tasks.

Popular Build Tools:

- Maven
- Gradle
- Ant

---

# Problems Solved by Automated Builds

## 1. Dependency Management

Without Maven:

```text
Download JARs manually
Add to project manually
Track versions manually
```

With Maven:

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <version>6.0.0</version>
</dependency>
```

Maven downloads everything automatically.

---

## 2. Consistent Builds

Every developer gets identical builds.

Example:

```bash
mvn package
```

Produces same result on all machines.

---

## 3. Automated Testing

Maven can execute tests automatically.

```bash
mvn test
```

---

## 4. Packaging

Creates deployable artifacts.

Examples:

```text
JAR
WAR
EAR
```

---

## 5. Deployment Automation

Artifacts can be deployed automatically.

```bash
mvn deploy
```

---

# Project Object Model (POM)

## What is POM?

POM stands for:

```text
Project Object Model
```

Maven project configuration is stored in:

```text
pom.xml
```

This file contains:

- Project Information
- Dependencies
- Plugins
- Build Configuration
- Repository Information

---

# Basic POM Structure

```xml
<project>

    <modelVersion>4.0.0</modelVersion>

    <groupId>com.company</groupId>

    <artifactId>demo-app</artifactId>

    <version>1.0</version>

</project>
```

---

# Important POM Elements

## groupId

Identifies organization.

```xml
<groupId>com.company</groupId>
```

---

## artifactId

Project name.

```xml
<artifactId>demo-app</artifactId>
```

---

## version

Project version.

```xml
<version>1.0</version>
```

---

## packaging

Artifact type.

```xml
<packaging>jar</packaging>
```

Possible values:

- jar
- war
- ear

---

# Maven Standard Directory Structure

Maven follows a predefined structure.

```text
project
│
├── pom.xml
│
├── src
│   ├── main
│   │   ├── java
│   │   └── resources
│   │
│   └── test
│       ├── java
│       └── resources
│
└── target
```

---

## src/main/java

Application source code.

```text
src/main/java
```

---

## src/main/resources

Configuration files.

```text
application.properties
```

---

## src/test/java

Test code.

```text
JUnit Tests
```

---

## target

Generated output.

```text
Compiled classes
JAR files
Reports
```

---

# Maven Build Lifecycle

A lifecycle is a sequence of build phases.

Main Lifecycle:

```text
validate
compile
test
package
verify
install
deploy
```

---

# Build Lifecycle Flow

```text
Validate
   ↓
Compile
   ↓
Test
   ↓
Package
   ↓
Verify
   ↓
Install
   ↓
Deploy
```

---

# validate Phase

Checks project structure.

```bash
mvn validate
```

Tasks:

- Verify pom.xml
- Validate project configuration

---

# compile Phase

Compiles Java source code.

```bash
mvn compile
```

Output:

```text
target/classes
```

---

# test Phase

Runs unit tests.

```bash
mvn test
```

Uses:

```text
JUnit
TestNG
```

---

# package Phase

Creates deployable artifact.

```bash
mvn package
```

Output:

```text
target/app.jar
```

or

```text
target/app.war
```

---

# verify Phase

Performs additional checks.

```bash
mvn verify
```

Examples:

- Integration Tests
- Quality Checks

---

# install Phase

Installs artifact into local repository.

```bash
mvn install
```

Stored in:

```text
~/.m2/repository
```

---

# deploy Phase

Publishes artifact to remote repository.

```bash
mvn deploy
```

Examples:

- Nexus
- Artifactory

---

# Parent POM

## What is Parent POM?

Used to share common configuration among multiple projects.

---

## Parent Project

```xml
<project>

    <groupId>com.company</groupId>

    <artifactId>parent-project</artifactId>

    <version>1.0</version>

    <packaging>pom</packaging>

</project>
```

---

## Child Project

```xml
<parent>

    <groupId>com.company</groupId>

    <artifactId>parent-project</artifactId>

    <version>1.0</version>

</parent>
```

---

# Advantages of Parent POM

- Centralized dependencies
- Shared plugins
- Shared properties
- Easier maintenance

---

# Dependency Scope

Scope controls dependency availability.

---

## Compile Scope (Default)

Available everywhere.

```xml
<scope>compile</scope>
```

Used during:

- Compile
- Test
- Runtime

---

## Provided Scope

Available during compile.

Not packaged.

```xml
<scope>provided</scope>
```

Example:

```xml
Servlet API
```

---

## Runtime Scope

Not needed for compile.

Needed at runtime.

```xml
<scope>runtime</scope>
```

Example:

```xml
MySQL Driver
```

---

## Test Scope

Used only for testing.

```xml
<scope>test</scope>
```

Example:

```xml
JUnit
```

---

# Transitive Dependencies

Maven automatically downloads dependent libraries.

Example:

```text
Project
  ↓
Spring Boot
  ↓
Spring Core
  ↓
Logging Libraries
```

Adding Spring Boot automatically downloads all required dependencies.

---

# Version Conflicts

Problem:

Two libraries require different versions.

Example:

```text
Library A → Log4j 1.0

Library B → Log4j 2.0
```

Which version should Maven use?

---

# Maven Conflict Resolution

Maven follows:

```text
Nearest Definition Wins
```

Example:

```text
Project
 ├── A → C v1.0
 └── B → C v2.0
```

Nearest dependency is selected.

---

# Dependency Management

Used to control dependency versions centrally.

---

## Example

```xml
<dependencyManagement>

    <dependencies>

        <dependency>

            <groupId>org.springframework</groupId>

            <artifactId>spring-core</artifactId>

            <version>6.0.0</version>

        </dependency>

    </dependencies>

</dependencyManagement>
```

---

## Child POM

```xml
<dependency>

    <groupId>org.springframework</groupId>

    <artifactId>spring-core</artifactId>

</dependency>
```

Version inherited automatically.

---

# Maven Plugins

## What are Plugins?

Plugins provide functionality to Maven.

Examples:

- Compile code
- Run tests
- Create JAR
- Create Docker images

---

# Maven Compiler Plugin

Compiles Java code.

```xml
<plugin>

    <groupId>org.apache.maven.plugins</groupId>

    <artifactId>maven-compiler-plugin</artifactId>

    <version>3.11.0</version>

</plugin>
```

---

## Configure Java Version

```xml
<configuration>

    <source>17</source>

    <target>17</target>

</configuration>
```

---

# Maven Surefire Plugin

Used for Unit Testing.

```xml
<plugin>

    <groupId>org.apache.maven.plugins</groupId>

    <artifactId>maven-surefire-plugin</artifactId>

</plugin>
```

Run:

```bash
mvn test
```

Supports:

- JUnit
- TestNG

---

# Maven Shade Plugin

Creates Uber/Fat JAR.

---

## What is Uber JAR?

A single JAR containing:

- Application code
- Dependencies

Example:

```text
app.jar
```

Contains everything required to run.

---

## Configuration

```xml
<plugin>

    <groupId>org.apache.maven.plugins</groupId>

    <artifactId>maven-shade-plugin</artifactId>

</plugin>
```

Build:

```bash
mvn package
```

---

# Maven Wrapper (mvnw)

## What is Maven Wrapper?

Wrapper allows projects to use a specific Maven version.

Files:

```text
mvnw
mvnw.cmd
.mvn/
```

Run:

```bash
./mvnw clean package
```

Benefits:

- No Maven installation required
- Consistent Maven version

---

# Maven and Docker Integration

---

# dockerfile-maven-plugin

Used to build Docker images using Maven.

Example:

```xml
<plugin>

    <groupId>com.spotify</groupId>

    <artifactId>dockerfile-maven-plugin</artifactId>

</plugin>
```

Build Docker image:

```bash
mvn package dockerfile:build
```

---

# Dockerizing Maven Applications

## Spring Boot Example

### Dockerfile

```dockerfile
FROM eclipse-temurin:17

COPY target/app.jar app.jar

ENTRYPOINT ["java","-jar","app.jar"]
```

---

# Build Application

```bash
mvn package
```

---

# Build Docker Image

```bash
docker build -t spring-app .
```

---

# Run Container

```bash
docker run -p 8080:8080 spring-app
```

---

# Maven + Docker Workflow

```text
Source Code
      ↓
mvn package
      ↓
JAR Generated
      ↓
Docker Build
      ↓
Docker Image
      ↓
Docker Registry
      ↓
Deployment
```

---

# Pushing Artifacts to Registries

---

# Maven Artifact Registry

Examples:

- Nexus Repository
- Artifactory
- GitHub Packages

Deploy:

```bash
mvn deploy
```

Artifact uploaded automatically.

---

# Docker Registry

Examples:

- Docker Hub
- GitHub Container Registry
- AWS ECR
- Azure Container Registry

---

## Login

```bash
docker login
```

---

## Tag Image

```bash
docker tag spring-app username/spring-app:v1
```

---

## Push Image

```bash
docker push username/spring-app:v1
```

---

# Complete Maven Build Commands

## Clean Project

```bash
mvn clean
```

Deletes:

```text
target/
```

---

## Validate

```bash
mvn validate
```

---

## Compile

```bash
mvn compile
```

---

## Test

```bash
mvn test
```

---

## Package

```bash
mvn package
```

---

## Verify

```bash
mvn verify
```

---

## Install

```bash
mvn install
```

---

## Deploy

```bash
mvn deploy
```

---

# Viva Questions

## What is Maven?

A build automation and dependency management tool for Java projects.

---

## What is POM?

Project Object Model. Configuration file stored as pom.xml.

---

## What is Maven Lifecycle?

Sequence of build phases such as validate, compile, test, package, install, and deploy.

---

## Difference Between Package and Install?

Package → Creates JAR/WAR.

Install → Stores artifact in local Maven repository.

---

## What is Parent POM?

A POM used to share common configurations among multiple projects.

---

## What is Dependency Scope?

Controls when a dependency is available during build and runtime.

---

## What are Transitive Dependencies?

Dependencies automatically downloaded because another dependency requires them.

---

## What is Maven Surefire Plugin?

Plugin used for running unit tests.

---

## What is Maven Shade Plugin?

Plugin used to create an Uber/Fat JAR containing application code and dependencies.

---

## What is Maven Wrapper?

Tool that allows projects to use a specific Maven version without requiring Maven installation.

---

## How Maven Integrates with Docker?

Maven builds the application JAR and Docker packages it into a container image.

---

## What is dockerfile-maven-plugin?

A Maven plugin used to build Docker images during Maven build process.

---

## What is mvn deploy?

Uploads artifacts to remote repositories such as Nexus or Artifactory.

---

# End of Notes