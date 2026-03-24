pipeline {
    agent any

    tools {
        maven 'MAVEN'
        jdk 'JAVA17'
    }

    environment {
        SONAR_HOST_URL = "http://192.168.160.128:9000/"
        SONAR_TOKEN = "sqa_115965629ad3898bdcc8be201fdae28d98fc0054"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/sundar-techops/CI-CD-Project-using-Java-Web-Application.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                sh '''
                mvn sonar:sonar \
                -Dsonar.projectKey=ci-cd \
                -Dsonar.host.url=$SONAR_HOST_URL \
                -Dsonar.login=$SONAR_TOKEN
                '''
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t java-ci-cd-app .'
            }
        }

        stage('Docker Deploy') {
            steps {
                sh '''
                docker rm -f app || true
                docker run -d -p 8081:8080 --name app --restart=always java-ci-cd-app
                '''
            }
        }
    }
}
