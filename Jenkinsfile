pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME' // This matches the name you gave in Jenkins Tools
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('MuleSoft Unit Test & Build') {
            steps {
                // 'bat' is for Windows commands. 
                // This compiles the code and runs MUnit tests.
                bat 'mvn clean install -DskipTests' 
            }
        }
    }
    
    post {
        success {
            echo 'Build Completed Successfully!'
        }
        failure {
            echo 'Build Failed. Check the logs and your Mule code.'
        }
    }
}
