pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME' 
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('MuleSoft Build') {
            steps {
                bat 'mvn clean install -DskipTests' 
            }
        }
    }
}
