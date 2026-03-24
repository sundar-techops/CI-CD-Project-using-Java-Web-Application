pipeline {
    agent any

    tools {
        maven 'MAVEN'
        jdk 'JAVA17'
    }

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean package'
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
                docker run -d -p 8081:8080 --name app java-ci-cd-app
                '''
            }
        }
    }
}
