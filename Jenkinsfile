pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/YOUR_USERNAME/basic-java-app.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package -DskipTests'
            }
        }

        stage('Run') {
            steps {
                bat 'java -jar target/basic-java-app-1.0-SNAPSHOT.jar'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: false
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}