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

        stage('Build & Deploy to CloudHub 2.0') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'anypoint-credentials', 
                                     usernameVariable: 'Satishganta', 
                                     passwordVariable: 'Possibleme22$$')]) {
                        
                        // Combined Java 17 permissions
                        withEnv(["MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED --add-opens java.base/java.lang=ALL-UNNAMED"]) {
                            
                            // We run 'clean deploy' together. This builds the JAR and pushes to Exchange/CloudHub in one go.
                            bat "mvn clean deploy -DskipTests " +
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
            echo 'FAILED: Check logs for Java, Maven, or Exchange errors.'
        }
    }
}
