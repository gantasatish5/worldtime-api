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
                    // Added java.util permission for Maven Plugin 3.8.2
                    withEnv(["MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED"]) {
                        bat 'mvn clean install -DskipTests -U -Dmaven.repo.local=C:\\Users\\ganta\\.m2\\repository'
                    }
                }
            }
        }

        stage('Deploy to CloudHub 2.0') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'anypoint-credentials', 
                                     usernameVariable: 'Satishganta', 
                                     passwordVariable: 'Possibleme22$$')]) {
                        
                        // Apply the same MAVEN_OPTS here
                        withEnv(["MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED"]) {
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
        success {
            echo 'SUCCESS: API build complete and deployment initiated to CloudHub 2.0!'
        }
        failure {
            echo 'FAILED: Deployment failed. Check the logs above.'
        }
    }
}
