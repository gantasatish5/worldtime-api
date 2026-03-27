pipeline {
    agent any
    tools {
        maven 'MAVEN_HOME' 
        jdk 'JAVA_HOME' 
    }
    stage('MuleSoft Build') {
            steps {
                script {
                    // This opens the internal Java modules that the Mule plugin is complaining about
                    withEnv(['MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED']) {
                        bat 'mvn clean install -DskipTests -U -Dmaven.repo.local=C:\\Users\\ganta\\.m2\\repository'
                    }
                }
            }
        }
    }
    post {
        success { echo 'SUCCESS: MuleSoft API Build Complete!' }
        failure { echo 'FAILED: Check logs for errors.' }
    }
}
