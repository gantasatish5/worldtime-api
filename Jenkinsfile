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
                    // Ensure ID matches exactly what you created in Jenkins Credentials
                    withCredentials([usernamePassword(credentialsId: 'anypoint-credentials', 
                                     usernameVariable: 'Satishganta', 
                                     passwordVariable: 'Possibleme22$$')]) {
                        
                        // We use double quotes to allow Jenkins to swap ${AP_USER} for the real value
                        withEnv(["MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED"]) {
                            bat "mvn mule:deploy -DskipTests -Danypoint.username=${env.AP_USER} -Danypoint.password=${env.AP_PASS} -Dmaven.repo.local=C:\\Users\\ganta\\.m2\\repository"
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
