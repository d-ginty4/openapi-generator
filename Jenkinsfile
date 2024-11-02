pipeline {
    agent any

    environment {
        JAVA_HOME = tool name: 'JDK11'   // Ensure this matches your Jenkins configuration
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from SCM (like Git)
                git branch: 'master', url: 'https://github.com/d-ginty4/openapi-generator.git'
            }
        }
        
        stage('Build') {
            steps {
                // Use Maven to build the project and package it as a JAR
                sh 'mvn clean install'
            }
        }
        
        stage('Archive JAR') {
            steps {
                // Archive the generated JAR file to make it available as a build artifact
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        always {
            // This will run at the end of the pipeline, regardless of success or failure
            echo 'Pipeline finished.'
        }
    }
}
