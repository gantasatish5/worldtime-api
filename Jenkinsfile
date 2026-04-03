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

        stage('MuleSoft Build & Deploy') {
            steps {
                script {
                    withCredentials([usernamePassword(
                        credentialsId: 'anypoint-credentials', 
                        usernameVariable: 'AP_USER', 
                        passwordVariable: 'AP_PASS'
                    )]) {
                        
                        withEnv(["MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED --add-opens java.base/java.lang=ALL-UNNAMED"]) {
                            
                            bat """
mvn clean package mule:deploy -DskipTests ^
-Danypoint.username=%AP_USER% ^
-Danypoint.password=%AP_PASS% ^
-Dmaven.repo.local=C:/Users/ganta/.m2/repository
"""
                        }
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: API is now deploying to CloudHub 2.0!'
        }
        failure {
            echo 'FAILED: Deployment failed. Check logs.'
        }
    }
}
