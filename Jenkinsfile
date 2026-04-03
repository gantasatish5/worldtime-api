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
                    // Use AP_USER and AP_PASS as labels
                    withCredentials([usernamePassword(credentialsId: 'anypoint-credentials', 
                                     usernameVariable: 'Satishganta', 
                                     passwordVariable: 'Possibleme22$$')]) {
                        
                        withEnv(["MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED --add-opens java.base/java.lang=ALL-UNNAMED"]) {
                            
                            // Use the variables AP_USER and AP_PASS here
                            bat "mvn clean mule:deploy -DskipTests " +
                                "-Danypoint.username=${AP_USER} " + 
                                "-Danypoint.password=${AP_PASS} " +
                                "-Dmaven.repo.local=C:\\Users\\ganta\\.m2\\repository"
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
            echo 'FAILED: Check for credentials or configuration errors.'
        }
    }
}
