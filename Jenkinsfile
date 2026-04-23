pipeline {
    agent any
    
    tools {
        jdk 'JDK25'     // Name exactly as configured in Jenkins
        maven 'Maven3.9' // Name exactly as configured in Jenkins
    }
    
    stages {
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
                bat 'mvn package'
            }
        }
        
        stage('Verify') {
            steps {
                bat 'java -jar target/basic-java-app-1.0-SNAPSHOT.jar'
            }
        }
    }
    
    post {
        always {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
        success {
            echo '🎉 Pipeline SUCCESS! Download JAR from Artifacts.'
        }
        failure {
            echo '❌ Pipeline FAILED. Check Maven/Java logs.'
        }
    }
}
