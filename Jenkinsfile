pipeline {
    agent any

    environment {
        
        EMAIL_RECIPIENT = 'roshandeepsingh75@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the React application...' 
                echo 'Task: Install dependencies using npm/yarn and build the React app using Webpack or Vite.'
                echo 'Tool Used: npm'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                echo 'Task: Execute unit tests using Jest and integration tests with React Testing Library.'
                echo 'Tool Used: Jest'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing static code analysis...'
                echo 'Task: Run ESLint and SonarQube to analyze code quality and adherence to best practices.'
                echo 'Tool Used: ESLint, SonarQube'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
                echo 'Task: Scan dependencies for known vulnerabilities using OWASP Dependency Check.'
                echo 'Tool Used: OWASP Dependency Check'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                echo 'Task: Build a Docker image and deploy the React app to the staging server using Nginx.'
                echo 'Tool Used: Docker, Nginx'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running end-to-end tests on staging...'
                echo 'Task: Execute Selenium WebDriver tests to validate application workflows in staging.'
                echo 'Tool Used: Selenium WebDriver'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                echo 'Task: Push Docker image to production and serve the React app using Nginx.'
                echo 'Tool Used: Docker, Nginx'
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
