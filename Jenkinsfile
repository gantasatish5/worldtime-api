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
                    // This 'add-opens' flag is the specific fix for the IllegalAccessError on Java 17
                    withEnv(['MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED']) {
                        bat 'mvn clean install -DskipTests -U -Dmaven.repo.local=C:\\Users\\ganta\\.m2\\repository'
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: MuleSoft API Build Complete!'
        }
        failure {
            echo 'FAILED: Check logs for errors.'
        }
    }
}
