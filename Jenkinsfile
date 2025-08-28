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
        dir('Spring-demo') {   // run mvn inside the folder where pom.xml is
            bat 'mvn clean package'
        }
    }
}

stage('Test') {
    steps {
        dir('Spring-demo') {
            bat 'mvn test'
        }
    }
}

stage('Run') {
    steps {
        dir('Spring-demo/target') { // Go to the target folder
            sh '''
                JAR=$(ls *.jar | head -n 1)
                echo "Running $JAR"
                java -jar "$JAR"
            '''
        }
    }
}



    }
}
