# CI/CD with Jenkins

---

# 1. Introduction to Jenkins

## What is Jenkins?

Jenkins is an open-source automation server used for:

- Continuous Integration (CI)
- Continuous Delivery (CD)
- Continuous Deployment

It automates:

- Code building
- Testing
- Packaging
- Deployment

Jenkins is one of the most widely used DevOps tools.

---

# Why Jenkins?

Without Jenkins:

```text
Developer
   ↓
Manual Build
   ↓
Manual Testing
   ↓
Manual Deployment
```

With Jenkins:

```text
Developer Pushes Code
         ↓
Jenkins Automatically
         ↓
Build
         ↓
Test
         ↓
Package
         ↓
Deploy
```

Benefits:

- Faster releases
- Fewer human errors
- Better code quality
- Continuous feedback

---

# Jenkins Architecture

Jenkins follows a:

```text
Master-Agent Architecture
```

---

# Master Node

The Jenkins Master:

- Provides Web UI
- Schedules jobs
- Manages plugins
- Controls agents
- Stores configurations

---

# Agent Nodes

Agents perform actual work.

Examples:

- Compile code
- Run tests
- Build Docker images
- Deploy applications

---

# Architecture Diagram

```text
                Jenkins Master
                       │
      ┌────────────────┼────────────────┐
      │                │                │
      ▼                ▼                ▼

 Agent 1         Agent 2         Agent 3

 Java Build      Docker Build    Testing
```

---

# Advantages of Master-Agent Model

- Distributed builds
- Better performance
- Scalability
- Parallel execution

---

# Jenkins Installation

---

## Install on Docker

```bash
docker run -d \
-p 8080:8080 \
-p 50000:50000 \
--name jenkins \
jenkins/jenkins:lts
```

Access:

```text
http://localhost:8080
```

---

# Unlock Jenkins

Get initial password:

```bash
docker exec jenkins cat \
/var/jenkins_home/secrets/initialAdminPassword
```

---

# Jenkins UI Overview

Main Sections:

```text
Dashboard
New Item
Build History
Manage Jenkins
Manage Plugins
Credentials
Nodes
```

---

# Plugin Management

Plugins extend Jenkins functionality.

Examples:

- Git Plugin
- Docker Plugin
- Maven Integration
- Blue Ocean
- Pipeline Plugin

---

# Installing Plugins

Navigate:

```text
Manage Jenkins
   ↓
Plugins
   ↓
Available Plugins
```

Install required plugin.

---

# Security in Jenkins

---

# User Management

Create users:

```text
Manage Jenkins
   ↓
Manage Users
```

---

# Authentication Methods

Supported:

- Jenkins Database
- LDAP
- GitHub OAuth
- Google OAuth

---

# Role-Based Access Control (RBAC)

Permissions can be assigned.

Example:

```text
Admin
Developer
Viewer
```

---

# Best Security Practices

- Disable anonymous access
- Use HTTPS
- Use Role-Based Access
- Rotate credentials
- Update plugins

---

# Jenkins Jobs

Two major job types:

1. Freestyle Jobs
2. Pipeline Jobs

---

# Freestyle Jobs

Traditional Jenkins jobs.

Configuration done through GUI.

Example:

```text
Build Java Project
Run Shell Script
```

Advantages:

- Easy for beginners

Disadvantages:

- Hard to version control

---

# Pipeline Jobs

Pipeline defined as code.

Stored in:

```text
Jenkinsfile
```

Advantages:

- Version controlled
- Reusable
- Scalable

---

# Freestyle vs Pipeline

| Feature | Freestyle | Pipeline |
|----------|----------|-----------|
| GUI Based | Yes | No |
| Version Control | No | Yes |
| Scalability | Low | High |
| Recommended | No | Yes |

---

# Jenkins Pipelines

A pipeline defines CI/CD workflow.

Example:

```text
Checkout
   ↓
Build
   ↓
Test
   ↓
Package
   ↓
Deploy
```

---

# Declarative Pipeline Syntax

Most commonly used.

Example:

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {

            steps {

                echo 'Building'

            }
        }
    }
}
```

---

# Scripted Pipeline Syntax

Uses Groovy scripting.

Example:

```groovy
node {

    stage('Build') {

        echo 'Building'

    }
}
```

---

# Declarative vs Scripted

| Declarative | Scripted |
|------------|-----------|
| Easier | Flexible |
| Structured | Advanced |
| Recommended | Complex Workflows |

---

# Jenkinsfile Structure

Basic Structure:

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {

            steps {

            }
        }
    }
}
```

---

# Parameters

Used for user input.

Example:

```groovy
parameters {

    string(
      name: 'VERSION',
      defaultValue: '1.0'
    )
}
```

Run:

```text
Build with Parameters
```

---

# Environment Variables

Global variables.

Example:

```groovy
environment {

    APP_NAME = "FoodieApp"

}
```

Access:

```groovy
echo "${APP_NAME}"
```

---

# Multi-Branch Pipelines

Automatically build Git branches.

Example:

```text
main
develop
feature/login
feature/payment
```

Jenkins automatically discovers branches.

---

# Pipeline Stages

---

# Stage 1: Checkout Code

```groovy
stage('Checkout') {

    steps {

        git 'https://github.com/user/repo.git'

    }
}
```

---

# Stage 2: Build

```groovy
stage('Build') {

    steps {

        sh 'mvn compile'

    }
}
```

---

# Stage 3: Test

```groovy
stage('Test') {

    steps {

        sh 'mvn test'

    }
}
```

---

# Stage 4: Package

```groovy
stage('Package') {

    steps {

        sh 'mvn package'

    }
}
```

---

# Post Actions

Executed after pipeline completion.

Example:

```groovy
post {

    always {

        echo 'Finished'

    }

    success {

        echo 'Success'

    }

    failure {

        echo 'Failed'

    }
}
```

---

# Managing Artifacts

Artifacts are generated outputs.

Examples:

```text
JAR
WAR
Reports
Logs
```

Archive:

```groovy
archiveArtifacts artifacts: '*.jar'
```

---

# Docker and Jenkins Integration

Jenkins can:

- Build Docker Images
- Push Images
- Deploy Containers

---

# Building Docker Images

```groovy
stage('Docker Build') {

    steps {

        sh 'docker build -t app .'

    }
}
```

---

# Docker Inside Jenkins Agents

Agent must have:

```text
Docker Installed
Docker Permission
```

Verify:

```bash
docker version
```

---

# Docker Plugins

Popular Plugins:

- Docker Plugin
- Docker Pipeline Plugin
- Docker Commons

---

# Publishing Images to Docker Hub

Login:

```bash
docker login
```

Pipeline:

```groovy
sh 'docker push username/app'
```

---

# Publishing to GHCR

GitHub Container Registry:

```bash
ghcr.io/user/app
```

Push:

```groovy
sh 'docker push ghcr.io/user/app'
```

---

# Jenkins and GitHub Integration

---

# Connect GitHub Repository

Install:

```text
Git Plugin
GitHub Plugin
```

Configure repository URL.

---

# GitHub Credentials

Store:

```text
Username
PAT Token
SSH Key
```

Inside:

```text
Manage Jenkins
   ↓
Credentials
```

---

# Backup and Restore

Important Jenkins Data:

```text
Jobs
Plugins
Credentials
Jenkinsfile Configurations
```

Stored in:

```text
JENKINS_HOME
```

---

# Backup

```bash
tar -czvf backup.tar.gz \
/var/jenkins_home
```

---

# Restore

```bash
tar -xzvf backup.tar.gz
```

Restart Jenkins.

---

# Pipeline Best Practices

- Keep pipelines simple
- Use Jenkinsfile
- Use credentials securely
- Avoid hardcoded passwords
- Use shared libraries
- Archive artifacts
- Use parallel stages

---

# Jenkins and Maven

---

# Maven Installation in Jenkins

Navigate:

```text
Manage Jenkins
   ↓
Global Tool Configuration
```

Add Maven.

Example:

```text
Maven 3.9
```

---

# Global Tool Configuration

Configure:

```text
JDK
Maven
Git
Docker
```

---

# Running Maven Builds

Pipeline:

```groovy
stage('Build') {

    steps {

        sh 'mvn clean package'

    }
}
```

---

# Complete Maven Pipeline

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {

            steps {

                sh 'mvn clean package'

            }
        }
    }
}
```

---

# Code Coverage Reports

Popular Tools:

- JaCoCo
- Cobertura

Generate:

```bash
mvn test jacoco:report
```

---

# Publish Coverage Report

```groovy
publishHTML(...)
```

---

# Test Reports

JUnit Reports:

```groovy
junit '**/target/surefire-reports/*.xml'
```

Jenkins displays:

```text
Passed Tests
Failed Tests
Coverage
```

---

# Triggering Builds

---

# Poll SCM

Jenkins checks repository periodically.

```groovy
pollSCM('* * * * *')
```

Checks every minute.

---

# GitHub Webhook

Preferred method.

GitHub notifies Jenkins immediately.

Workflow:

```text
GitHub Push
     ↓
Webhook
     ↓
Jenkins Build
```

---

# Pipeline Libraries

Shared reusable code.

Example:

```groovy
@Library('shared-lib')
```

Benefits:

- Reusability
- Standardization
- Easier maintenance

---

# Jenkins Agents

---

# SSH Agents

Connect through SSH.

```text
Master
   ↓ SSH
Agent
```

---

# SFTP Agents

Used for file transfers.

Example:

```text
Artifact Deployment
```

---

# Container-Based Agents

Run builds inside containers.

Example:

```groovy
agent {

    docker {

        image 'maven:3.9'
    }
}
```

Benefits:

- Isolation
- Consistency
- Portability

---

# Deployments to Servers

Example:

```groovy
stage('Deploy') {

    steps {

        sh '''
        scp app.jar user@server:/opt/app
        '''
    }
}
```

---

# Deployments to Cloud

Supported:

- AWS
- Azure
- Google Cloud
- Kubernetes

Example:

```groovy
sh 'kubectl apply -f deployment.yaml'
```

---

# Complete Jenkins CI/CD Flow

```text
Developer Pushes Code
          ↓
GitHub Webhook
          ↓
Jenkins Pipeline Triggered
          ↓
Checkout Source Code
          ↓
Maven Build
          ↓
Run Tests
          ↓
Generate Reports
          ↓
Build Docker Image
          ↓
Push Image
          ↓
Deploy Application
          ↓
Production
```

---

# Sample Complete Jenkinsfile

```groovy
pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/user/repo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t app .'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying'
            }
        }
    }

    post {

        success {
            echo 'Deployment Successful'
        }

        failure {
            echo 'Pipeline Failed'
        }
    }
}
```

---

# Viva Questions

## What is Jenkins?

An open-source automation server used for CI/CD.

---

## What is Jenkins Master?

Central controller that manages jobs, agents, and pipelines.

---

## What is Jenkins Agent?

A machine that executes build tasks.

---

## Difference Between Freestyle and Pipeline?

Freestyle → GUI-based.

Pipeline → Code-based.

---

## What is Jenkinsfile?

A file containing pipeline definition.

---

## What is Declarative Pipeline?

Structured pipeline syntax recommended for most projects.

---

## What is Scripted Pipeline?

Groovy-based flexible pipeline syntax.

---

## What is Multi-Branch Pipeline?

Automatically builds multiple Git branches.

---

## What is Poll SCM?

Periodically checks repository changes.

---

## What is GitHub Webhook?

GitHub event that instantly triggers Jenkins builds.

---

## What is JaCoCo?

Java code coverage reporting tool.

---

## How Jenkins Integrates with Docker?

Builds, pushes, and deploys Docker images using pipelines.

---

## Where Jenkins Stores Data?

```text
JENKINS_HOME
```

---

## What are Shared Libraries?

Reusable pipeline code shared across projects.

---

## What are Container-Based Agents?

Agents running inside Docker containers.

---

# End of Notes