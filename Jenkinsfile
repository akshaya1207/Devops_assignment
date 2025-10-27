pipeline {
    agent any

    tools {
        // 👇 Make Jenkins use your configured Maven installation
        maven 'Maven_3.9.11'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/akshaya1207/Devops_assignment.git'
            }
        }

        stage('Build & Test') {
            steps {
                script {
                    // Detect OS and run the correct Maven command
                    if (isUnix()) {
                        sh 'mvn clean test package'
                    } else {
                        bat 'mvn clean test package'
                    }
                }
            }
        }

        stage('Archive Artifact') {
            steps {
                // ✅ Use your actual JAR name here
                archiveArtifacts artifacts: 'target/library-system-1.0.0.jar', fingerprint: true
            }
        }

        stage('Publish Test Results') {
            steps {
                junit 'target/surefire-reports/*.*
