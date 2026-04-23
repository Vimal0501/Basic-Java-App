pipeline {
    agent any
    
    tools {
        maven 'Maven'  // Make sure this is configured in Jenkins Global Tool Configuration
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
                bat 'mvn package -DskipTests'
            }
        }
        
        stage('Verify') {
            steps {
                bat 'java -jar target/basic-java-app-1.0-SNAPSHOT.jar'
                echo 'Application executed successfully!'
            }
        }
    }
    
    post {
        always {
            archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: false
        }
        success {
            echo 'Pipeline completed successfully! Check archived JAR file.'
        }
        failure {
            echo 'Pipeline failed. Check logs above.'
        }
    }
}
