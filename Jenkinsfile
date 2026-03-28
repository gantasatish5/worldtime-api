pipeline {
    agent any

    tools {
        // Must match the name defined in Manage Jenkins -> Tools
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
                    // Java 17 fix to allow the plugin to access internal JAR protocols
                    withEnv(["MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED"]) {
                        bat 'mvn clean install -DskipTests -U -Dmaven.repo.local=C:\\Users\\ganta\\.m2\\repository'
                    }
                }
            }
        }

        stage('Deploy to CloudHub 2.0') {
            steps {
                script {
                    // This pulls your username and password from the Jenkins credential 'anypoint-credentials'
                    withCredentials([usernamePassword(credentialsId: 'anypoint-credentials', 
                                     usernameVariable: 'Satishganta', 
                                     passwordVariable: 'Possibleme22$$')]) {
                        
                        withEnv(["MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED"]) {
                            // This command injects the credentials and tells Maven where the JAR file is
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
            echo 'FAILED: Check the console output above for Maven or Java errors.'
        }
    }
}
