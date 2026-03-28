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
                    withEnv(["MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED"]) {
                        bat 'mvn clean install -DskipTests -U -Dmaven.repo.local=C:\\Users\\ganta\\.m2\\repository'
                    }
                }
            }
        }

        stage('Deploy to CloudHub 2.0') {
            steps {
                script {
                    // ID must match exactly what you created in Jenkins Credentials manager
                    withCredentials([usernamePassword(credentialsId: 'anypoint-credentials', 
                                     usernameVariable: 'Satishganta', 
                                     passwordVariable: 'Possibleme22$$')]) {
                        
                        withEnv(["MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED"]) {
                            // Passing credentials from Jenkins variables into Maven placeholders
                            bat "mvn mule:deploy -DskipTests " +
                                "-Danypoint.username=${Satishganta} " +
                                "-Danypoint.password=${Possibleme22$$} " +
                                "-Dmule.artifact=target/schduler-1.0.0-SNAPSHOT-mule-application.jar " +
                                "-Dmaven.repo.local=C:\\Users\\ganta\\.m2\\repository"
                        }
                    }
                }
            }
        }
    }

    post {
        success { echo 'SUCCESS: API is deploying to CloudHub 2.0!' }
        failure { echo 'FAILED: Check logs for errors.' }
    }
}
