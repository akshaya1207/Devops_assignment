pipeline {
    agent any

    tools {
        // Make sure this matches the name configured in Jenkins
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
                archiveArtifacts artifacts: 'target/library-system-1.0.0.jar', fingerprint: true
            }
        }

        stage('Publish Test Results') {
            steps {
                // 👇 The missing quote fixed here
                junit 'target/surefire-reports/*.xml'
            }
        }
    }

    post {
        success {
            echo '✅ Build and Test Successful!'
        }
        failure {
            echo '❌ Build failed. Check console output.'
        }
    }
}
