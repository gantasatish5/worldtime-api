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
                    // Java 17 permissions required for the build
                    withEnv(["MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED --add-opens java.base/java.lang=ALL-UNNAMED"]) {
                        bat 'mvn clean install -DskipTests -U -Dmaven.repo.local=C:\\Users\\ganta\\.m2\\repository'
                    }
                }
            }
        }

        stage('Deploy to CloudHub 2.0') {
            steps {
                script {
                    // This pulls your credentials from the Jenkins 'anypoint-credentials' ID
                    withCredentials([usernamePassword(credentialsId: 'anypoint-credentials', 
                                     usernameVariable: 'Satishganta', 
                                     passwordVariable: 'Possibleme22$$')]) {
                        
                        withEnv(["MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED --add-opens java.base/java.lang=ALL-UNNAMED"]) {
                            
                            // CHANGED GOAL: Using 'deploy' instead of 'mule:deploy' for CloudHub 2.0
                            // This pushes the asset to Exchange and then to Runtime Manager
                            bat "mvn deploy -DskipTests " +
                                "-Danypoint.username=${Satishganta} " +
                                "-Danypoint.password=${Possibleme22$$} " +
                                "-Dmaven.repo.local=C:\\Users\\ganta\\.m2\\repository"
                        }
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: API Published to Exchange and Deployment started in CloudHub 2.0!'
        }
        failure {
            echo 'FAILED: Check logs for Java, Maven, or Exchange/Permission errors.'
        }
    }
}
