pipeline {
    agent any 
    tools {
        maven 'my-maven'
        jdk 'my-jdk'
    }
    stages {        
        stage('Clone') {
            steps {
                git url: 'https://github.com/panthnaik/myservices.git', branch: 'service-registry'
            }
        }
        stage('Build') {
            steps {
                bat "mvn clean install -DskipTests"
            }
        }
        stage('Test') {
            steps {
                bat "mvn test"
            }
        }
        stage('Deploy') {
            steps { 
                bat "docker rm -f service-container"
                bat "docker rmi -f service-image"
                bat "docker build -t service-image ."
                bat "docker run -p 8761:8761 -d --name service-container service-image"
            }
        }
    }
}
