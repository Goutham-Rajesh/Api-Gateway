pipeline {
    agent any
    tools {
        maven 'my-maven'
        jdk 'my-jdk'
    }
    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/Goutham-Rajesh/Api-Gateway.git', branch: 'main'
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
                bat "docker rm -f api-container"
                bat "docker rm -f api-image"
                bat "docker build -t api-image ."
                bat "docker run -p 8761:8761 -d --name api-container api-image"
            }
        }
    }
}
