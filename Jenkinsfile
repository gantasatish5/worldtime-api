pipeline {
    agent any

    tools {
        // Points to your Maven 3.8.8 installation in Jenkins Global Tool Configuration
        maven 'MAVEN_HOME'
        // Points to your JDK 17 installation in Jenkins Global Tool Configuration
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
                    // Java 17 fix for the Mule Maven Plugin
                    withEnv(["MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED"]) {
                        bat 'mvn clean install -DskipTests -U -Dmaven.repo.local=C:\\Users\\ganta\\.m2\\repository'
                    }
                }
            }
        }

        stage('Deploy to CloudHub') {
            steps {
                script {
                    // This pulls your secrets from Jenkins. 
                    // Make sure you created a 'Username with Password' credential with ID: anypoint-credentials
                    withCredentials([usernamePassword(credentialsId: 'anypoint-credentials', 
                                     usernameVariable: 'Satishganta', 
                                     passwordVariable: 'Possibleme22$$')]) {
                        
                        withEnv(["MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED"]) {
                            // We explicitly tell Maven where the JAR file is using -Dmule.artifact
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
            echo 'SUCCESS: API is now deploying to CloudHub. Check Anypoint Runtime Manager.'
        }
        failure {
            echo 'FAILED: Deployment failed. Check the logs above for the error.'
        }
    }
}
