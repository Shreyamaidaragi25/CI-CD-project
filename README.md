# CI-CD-project
# Complete CI/CD Pipeline on AWS using Jenkins, Maven, SonarQube, Nexus & Tomcat

## Project Overview

This project demonstrates a complete end-to-end CI/CD pipeline implementation on AWS using industry-standard DevOps tools.

The pipeline automates:
- Source Code Management
- Build Automation
- Code Quality Analysis
- Artifact Management
- Application Deployment

---

# Architecture

GitHub → Jenkins → Maven → SonarQube → Nexus → Tomcat

---

# Tools & Technologies Used

| Tool | Purpose |
|------|----------|
| AWS EC2 | Infrastructure Hosting |
| GitHub | Source Code Management |
| Jenkins | CI/CD Automation |
| Maven | Build Management |
| SonarQube | Code Quality Analysis |
| Nexus Repository | Artifact Storage |
| Apache Tomcat | Application Deployment |
| Java | Application Runtime |

---

# AWS Infrastructure

Separate EC2 instances were used for:

- Jenkins Server
- SonarQube Server
- Nexus Repository Server
- Tomcat Application Server

---

# Ports Used

| Service | Port |
|---------|------|
| SSH | 22 |
| Jenkins | 8080 |
| SonarQube | 9000 |
| Nexus | 8081 |
| HTTP | 80 |

---

# Jenkins Setup

## Installed Components
- OpenJDK 21
- Jenkins
- Maven

## Jenkins Plugins
- Maven Integration Plugin
- SonarQube Scanner Plugin
- Nexus Artifact Uploader
- Git Plugin
- Pipeline Plugin
- Deploy to Container Plugin

---

# Maven Build Commands

```bash
mvn compile
mvn test
mvn package

**# Sample jenkins pipeline**
pipeline {
    agent any

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'main',
                url: 'YOUR_GITHUB_REPO'
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn compile'
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

        stage('Sonar Analysis') {
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

    }
}
