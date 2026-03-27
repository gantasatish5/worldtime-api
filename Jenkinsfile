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
        // We add -Dmaven.resolver.transport=wagon to fix the missing class error
        bat 'mvn clean install -DskipTests -U -Dmaven.repo.local=C:\\Users\\ganta\\.m2\\repository -Dmaven.resolver.transport=wagon'
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
