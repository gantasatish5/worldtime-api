pipeline {
    agent any

    tools {
        // This must match the Name you gave in Manage Jenkins -> Tools
        maven 'MAVEN_HOME' 
        jdk 'JAVA_HOME' 
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('MuleSoft Build') {
            steps {
                // Jenkins will now automatically set JAVA_HOME to JDK 17 before running this
                bat 'mvn clean install -DskipTests' 
            }
        }
    }
    
    post {
        success {
            echo 'MuleSoft API Build Successful!'
        }
        failure {
            echo 'Build Failed. Please check the Console Output for Java or Maven errors.'
        }
    }
}
