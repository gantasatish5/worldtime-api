pipeline {
    agent any

    stages {
        stage('Pull from GitHub') {
            steps {
                echo 'Successfully connected to GitHub!'
                checkout scm
            }
        }
        stage('MuleSoft Build') {
            steps {
                echo 'Building your worldtime-api...'
                // If you have Maven installed, you can add: bat 'mvn clean install'
            }
        }
    }
}
