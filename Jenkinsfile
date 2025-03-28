pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'react-app'
        DOCKER_CONTAINER = 'react-container'
        STAGING_SERVER = 'staging.example.com'
        PRODUCTION_SERVER = 'production.example.com'
        EMAIL_RECIPIENT = 'roshandeepsingh75@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the React application...'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing static code analysis...'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running end-to-end tests on staging...'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
            emailext to: "${EMAIL_RECIPIENT}",
                     subject: 'Pipeline Execution Successful',
                     body: 'The CI/CD pipeline has completed successfully. Logs are attached.',
                     attachLog: true
        }
        failure {
            echo 'Pipeline failed!'
            emailext to: "${EMAIL_RECIPIENT}",
                     subject: 'Pipeline Execution Failed',
                     body: 'The pipeline encountered an error. Review Jenkins logs for details.',
                     attachLog: true
        }
    }
}
