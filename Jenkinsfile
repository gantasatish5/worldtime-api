stage('Deploy to CloudHub') {
            steps {
                script {
                    // Pull credentials securely from Jenkins
                    withCredentials([usernamePassword(credentialsId: 'anypoint-credentials', 
                                     usernameVariable: 'Satishganta', 
                                     passwordVariable: 'Possibleme22$$')]) {
                        
                        // IMPORTANT: Use double quotes ("...") for the bat command
                        withEnv(['MAVEN_OPTS=--add-opens java.base/sun.net.www.protocol.jar=ALL-UNNAMED']) {
                            bat "mvn mule:deploy -DskipTests -Danypoint.username=${AP_USER} -Danypoint.password=${AP_PASS} -Dmaven.repo.local=C:\\Users\\ganta\\.m2\\repository"
                        }
                    }
                }
            }
        }
