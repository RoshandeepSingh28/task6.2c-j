pipeline {
    environment {
        EMAIL_RECIPIENT = 'roshandeepsingh75@gmail.com'
        USER_EMAIL = 'roshandeepsingh75@gmail.com'
    }

    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using Maven...'
                sh 'mvn clean package'
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Build Stage Completed',
                         body: 'The build stage has completed. Check Jenkins logs for details.'
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using JUnit...'
                sh 'mvn test'
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Unit and Integration Tests Completed',
                         body: 'The unit and integration tests have completed. Check Jenkins logs for details.'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing static code analysis using SonarQube...'
                sh 'mvn sonar:sonar'
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Code Analysis Completed',
                         body: 'The code analysis stage has completed. Check Jenkins logs for details.'
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP Dependency-Check...'
                sh 'mvn dependency-check:check'
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Security Scan Completed',
                         body: 'The security scan has completed. Check the Jenkins logs for details.'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment on AWS EC2...'
                sh 'scp target/myapp.jar ec2-user@staging-server:/opt/app/'
                sh 'ssh ec2-user@staging-server "systemctl restart myapp"'
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Deployment to Staging Completed',
                         body: 'Deployment to the staging environment has completed. Check Jenkins logs for details.'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging using Postman Newman...'
                sh 'newman run tests/postman_collection.json'
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Integration Tests on Staging Completed',
                         body: 'Integration tests on staging have completed. Check Jenkins logs for details.'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment on AWS EC2...'
                sh 'scp target/myapp.jar ec2-user@prod-server:/opt/app/'
                sh 'ssh ec2-user@prod-server "systemctl restart myapp"'
            }
            post {
                always {
                    mail to: "${USER_EMAIL}",
                         subject: 'Deployment to Production Completed',
                         body: 'Deployment to production has completed. Check Jenkins logs for details.'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
            emailext to: "${USER_EMAIL}",
                     subject: 'Pipeline Execution Successful',
                     body: 'The entire pipeline has completed successfully.',
                     attachLog: true
        }
        failure {
            echo 'Pipeline failed! Check the logs for more details.'
            mail to: "${USER_EMAIL}",
                 subject: 'Pipeline Execution Failed',
                 body: 'The pipeline has failed. Please check the Jenkins logs for more details.'
        }
    }
}
