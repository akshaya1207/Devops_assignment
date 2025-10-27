pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/akshaya1207/Devops_assignment.git'
            }
        }

        stage('Build & Test') {
            steps {
                script {
                    // Windows: use bat, Linux/macOS: use sh
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
                archiveArtifacts artifacts: 'target/LibraryBookStore-1.0-SNAPSHOT.jar', fingerprint: true
            }
        }

        stage('Publish Test Results') {
            steps {
                junit 'target/surefire-reports/*.xml'
            }
        }
    }

    post {
        success {
            echo 'Build and Test Successful!'
        }
        failure {
            echo 'Build failed. Check console output.'
        }
    }
}
