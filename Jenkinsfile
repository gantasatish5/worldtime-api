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
            credentialsId: 'anypoint-credentials',
            usernameVariable: 'AP_USER',
            passwordVariable: 'AP_PASS'
        )]) {
            // Using 'install' then 'mule:publish' skips the pre-deploy check
            bat """
            mvn clean install -DskipTests -Dmaven.repo.local=C:/Users/ganta/.m2/repository ^
            && mvn org.mule.tools.maven:mule-maven-plugin:3.8.2:exchange-publish ^
            -Danypoint.username=%AP_USER% ^
            -Danypoint.password=%AP_PASS% ^
            -Dmaven.repo.local=C:/Users/ganta/.m2/repository
            """
        }
    }
}

        stage('Deploy to CloudHub 2.0') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'anypoint-credentials',
                    usernameVariable: 'AP_USER',
                    passwordVariable: 'AP_PASS'
                )]) {
                    // This stage starts the app using the asset we just published
                    bat """
                    mvn mule:deploy -DskipTests ^
                    -Danypoint.username=%AP_USER% ^
                    -Danypoint.password=%AP_PASS% ^
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
