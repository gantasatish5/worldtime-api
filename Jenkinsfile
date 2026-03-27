pipeline {
    agent any

    tools {
        // We keep Java here, but we will call Maven manually below
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
                // We use the full path to your mvn.cmd to bypass Jenkins tool conflicts
                // We also add the aether connector fix directly in the command
                bat '"C:\\Program Files\\apache-maven-3.9.14\\bin\\mvn.cmd" clean install -DskipTests -U -Dmaven.repo.local=C:\\Users\\ganta\\.m2\\repository -Dmaven.resolver.transport=wagon -Daether.connector.basic.threads=1'
            }
        }
    }
    
    post {
        success {
            echo 'MuleSoft API Build Successful!'
        }
        failure {
            echo 'Build Failed. Checking for library conflicts...'
        }
    }
}
