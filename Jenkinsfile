pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/drhudson1/calculator.git'
            }
        }

        stage('Verify Files') {
            steps {
                bat 'dir'
                bat 'dir src'
                bat 'dir src\\main\\java\\com\\example'
                bat 'dir src\\test\\java\\com\\example'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('Unit Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Code Coverage') {
            steps {
                bat 'mvn jacoco:report'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package'
            }
        }

    }

    post {
        always {
            junit allowEmptyResults: true, testResults: '**/target/surefire-reports/*.xml'
        }
    }
}