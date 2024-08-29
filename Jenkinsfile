pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the project using Maven'
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit and integration tests using JUnit'
                script {
                    currentBuild.result = 'SUCCESS'
                }
            }
            post {
                always {
                    script {
                        emailext(
                            subject: "Jenkins Test Stage - ${currentBuild.result}",
                            body: "The test stage was a: ${currentBuild.result}.",
                            attachLog: true,
                            to: "logantraitschool@gmail.com"
                        )
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running code analysis using SonarQube'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP Dependency Check'
                script {
                    currentBuild.result = 'SUCCESS'
                }
            }
            post {
                always {
                    script {
                        emailext(
                            subject: "Jenkins Security Scan Stage - ${currentBuild.result}",
                            body: "The security scan stage was a: ${currentBuild.result}.",
                            attachLog: true,
                            to: "logantraitschool@gmail.com"
                        )
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging server AWS EC2 using AWS CLI'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment using JUnit'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server AWS EC2 using AWS CLI'
            }
        }
    }
}
