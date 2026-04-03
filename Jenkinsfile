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
                    // This creates the labels AP_USER and AP_PASS from your Jenkins credentials
                    withCredentials([usernamePassword(credentialsId: 'anypoint-credentials', 
                                     usernameVariable: 'Satishganta', 
                                     passwordVariable: 'Possibleme22$$')]) {
                        
                        withEnv(["MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED --add-opens java.base/java.lang=ALL-UNNAMED"]) {
                            
                            // Using \$ ensures Jenkins doesn't look for the variable before the command runs
                            bat "mvn clean mule:deploy -DskipTests " +
                                "-Danypoint.username=\$AP_USER " + 
                                "-Danypoint.password=\$AP_PASS " +
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
            echo 'FAILED: Deployment failed. Check the logs above.'
        }
    }
}
