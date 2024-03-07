pipeline {
    agent any

    environment {
        // Define your SonarCloud credentials as environment variables
        SONAR_CLOUD_TOKEN = credentials('sonarcloud-token')
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout your source code
                checkout scm
            }
        }

        stage('Build') {
    steps {
        // Use the configured Maven installation
        script {
            def mavenHome = tool 'Maven'
            sh "${mavenHome}/bin/mvn clean install"
        }
    }
}


        stage('SonarQube Analysis') {
            steps {
                // Run SonarQube Scanner with SonarCloud configuration
                withSonarQubeEnv('SonarCloud') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }

    post {
        success {
            // Add any additional steps to execute on successful build
            echo 'Build and analysis completed successfully!'
        }
        failure {
            // Add any additional steps to execute on build failure
            echo 'Build or analysis failed. Check the logs for details.'
        }
    }
}
