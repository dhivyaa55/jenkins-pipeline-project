pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the project using Maven...'
                sh 'mvn clean install'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using JUnit and Selenium...'
                sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis using SonarQube...'
                sh 'mvn sonar:sonar'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP Dependency-Check...'
                sh 'dependency-check.sh --scan .'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment on AWS EC2...'
                sh 'scp target/*.war user@staging-server:/path/to/deploy'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment...'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment on AWS EC2...'
                sh 'scp target/*.war user@prod-server:/path/to/deploy'
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            mail to: 'sdhivyaalakshmi@gmail.com',
                 subject: "Pipeline Success: ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                 body: "Pipeline completed successfully.\n\nCheck the Jenkins logs for details.",
                 attachLog: true
        }
        failure {
            mail to: 'sdhivyaalakshmi@gmail.com',
                 subject: "Pipeline Failed: ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                 body: "Pipeline failed. Please check the Jenkins logs for details.",
                 attachLog: true
        }
    }
}
