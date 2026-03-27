pipeline {
    agent any
    tools {
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
                // With Maven 3.8.8, all the "Missing Class" errors will disappear
                bat 'mvn clean install -DskipTests -U'
            }
        }
    }
    post {
        success { echo 'SUCCESS: MuleSoft API Build Complete!' }
        failure { echo 'FAILED: Check logs for errors.' }
    }
}
