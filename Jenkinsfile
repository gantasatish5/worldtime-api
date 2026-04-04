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

stage('Build & Publish to Exchange') {
    steps {
        withCredentials([usernamePassword(
            credentialsId: 'anypoint-connected-app',
            usernameVariable: 'CLIENT_ID',
            passwordVariable: 'CLIENT_SECRET'
        )]) {
            bat """
            mvn clean install -DskipTests -Dmaven.repo.local=C:/Users/ganta/.m2/repository ^
            && mvn mule:deploy -DskipTests ^
            -Danypoint.client_id=%CLIENT_ID% ^
            -Danypoint.client_secret=%CLIENT_SECRET% ^
            -DmuleDeploy=false ^
            -Dmaven.repo.local=C:/Users/ganta/.m2/repository
            """
        }
    }
}

        stage('Deploy to CloudHub 2.0') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'anypoint-connected-app',
                    usernameVariable: 'CLIENT_ID',
                    passwordVariable: 'CLIENT_SECRET'
                )]) {
                    bat """
                    mvn mule:deploy -DskipTests ^
                    -Danypoint.client_id=%CLIENT_ID% ^
                    -Danypoint.client_secret=%CLIENT_SECRET% ^
                    -Dmaven.repo.local=C:/Users/ganta/.m2/repository
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: API deployed to CloudHub 2.0'
        }
        failure {
            echo 'FAILED: Check logs carefully'
        }
    }
}
