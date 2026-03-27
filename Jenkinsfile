pipeline {
    agent any
    stages {
        stage('Pull from GitHub') {
            steps {
                echo 'Successfully pulled worldtime-api from GitHub!'
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building project...'
                // For MuleSoft, you will eventually add: bat 'mvn clean install'
            }
        }
    }
}
