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
                script {
                    // Java 17 fix for Mule Maven Plugin
                    withEnv(['MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED']) {
                        bat 'mvn clean install -DskipTests -U -Dmaven.repo.local=C:\\Users\\ganta\\.m2\\repository'
                    }
                }
            }
        }

        stage('Deploy to CloudHub') {
            steps {
                script {
                    // Pull credentials securely from Jenkins (ID must be 'anypoint-credentials')
                    withCredentials([usernamePassword(credentialsId: 'anypoint-credentials', 
                                     usernameVariable: 'Satishganta', 
                                     passwordVariable: 'Possibleme22$$')]) {
                        
                        // We use double quotes for the bat command to allow variable injection
                        withEnv(['MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED']) {
                            bat "mvn mule:deploy -DskipTests -Danypoint.username=${AP_USER} -Danypoint.password=${AP_PASS} -Dmaven.repo.local=C:\\Users\\ganta\\.m2\\repository"
                        }
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: MuleSoft API Built and Deployed to CloudHub!'
        }
        failure {
            echo 'FAILED: Check the console logs for errors.'
        }
    }
}
