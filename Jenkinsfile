pipeline {
    agent any

    tools {
        maven 'Maven 3.9.11'   // Name from Jenkins Global Tool Configuration
        jdk 'JDK 21'           // Name from Jenkins Global Tool Configuration
    }

    stages {

        stage('Clean Old Process') {
            steps {
                echo 'Stopping any old Spring Boot app on port 9090...'
                bat '''
                for /f "tokens=5" %%p in ('netstat -ano ^| findstr :9090 ^| findstr LISTENING') do taskkill /PID %%p /F
                exit 0
                '''
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project using Maven...'
                bat 'mvn clean package'
            }
        }

        stage('Run') {
            steps {
                echo 'Starting Spring Boot app on port 9090...'
                bat 'start /B java -jar target\\springboot-jenkins-demo-1.0.0.jar --server.port=9090'
            }
        }
    }
}
