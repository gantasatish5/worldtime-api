pipeline {
    agent any

    tools {
        // These must match the names in your Manage Jenkins -> Tools configuration
        maven 'MAVEN_HOME'
        jdk 'JAVA_HOME'
    }

    stages {
        stage('Checkout') {
            steps {
                // Pulls the latest code from your GitHub repo
                checkout scm
            }
        }

        stage('MuleSoft Build & Deploy') {
            steps {
                script {
                    // This block connects to the secret credential you created in Jenkins
                    withCredentials([usernamePassword(credentialsId: 'anypoint-credentials', 
                                     usernameVariable: 'Satishganta', 
                                     passwordVariable: 'Possibleme22$$')]) {
                        
                        // These Java 17 permissions are required for the Mule Maven Plugin 3.8.2
                        withEnv(["MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED --add-opens java.base/java.lang=ALL-UNNAMED"]) {
                            
                            // EXPLAINING THE COMMAND:
                            // clean: clears old files
                            // install: builds the JAR and puts it in local .m2 (fixes the "Artifact Not Found" error)
                            // deploy: uploads to Anypoint Exchange AND triggers CloudHub 2.0 deployment
                            bat "mvn clean install deploy -DskipTests " +
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
            echo 'CONGRATULATIONS: Build passed, asset uploaded to Exchange, and CloudHub 2.0 deployment started!'
        }
        failure {
            echo 'FAILED: Check the log for a 401 (Auth), 409 (Version Conflict), or 400 (Region) error.'
        }
    }
}
