pipeline {
    agent any

    tools {
        maven 'Maven_3.9.11'  // your Maven tool name
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/akshaya1207/Devops_assignment.git'
            }
        }

        stage('Build & Package') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'mvn clean package -DskipTests'
                    } else {
                        bat 'mvn clean package -DskipTests'
                    }
                }
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Build Successful (Tests skipped)'
        }
        failure {
            echo '❌ Build failed. Check console output.'
        }
    }
}
