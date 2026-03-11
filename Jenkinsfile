pipeline {

    agent any

    stages {

        stage('Confirm Jenkinsfile Version') {
            steps {
                echo 'NEW JENKINSFILE LOADED - drhudson1/calculator main branch'
            }
        }

        stage('Verify Files') {
            steps {
                bat 'dir'
                bat 'dir Calculator'
                bat 'dir Calculator\\src'
                bat 'dir Calculator\\src\\main\\java\\com\\example'
                bat 'dir Calculator\\src\\test\\java\\com\\example'
            }
        }

        stage('Build') {
            steps {
                dir('Calculator') {
                    bat 'mvn clean compile'
                }
            }
        }

        stage('Unit Test') {
            steps {
                dir('Calculator') {
                    bat 'mvn test'
                }
            }
        }

        stage('Code Coverage') {
            steps {
                dir('Calculator') {
                    bat 'mvn jacoco:report'
                }
            }
        }

        stage('Package') {
            steps {
                dir('Calculator') {
                    bat 'mvn package'
                }
            }
        }

    }

    post {
        always {
            junit allowEmptyResults: true, testResults: 'Calculator/target/surefire-reports/*.xml'
        }
    }
}