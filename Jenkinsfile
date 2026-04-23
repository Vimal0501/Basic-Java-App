pipeline {
    agent any
    
    tools {
        jdk 'JDK_25'     // ← Exact name from your error
        maven 'Maven'    // ← Exact name from your error
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
            echo '🎉 SUCCESS! JAR ready for download.'
        }
        failure {
            echo '❌ FAILED. Check Java/Maven paths.'
        }
    }
}
