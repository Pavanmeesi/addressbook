pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "mymaven"
    }

    stages {
        stage('compile') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/Pavanmeesi/addressbook.git'

                // Run Maven on a Unix agent.
                sh "mvn compile"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('UnitTest') {
            steps {
                // Get some code from a GitHub repository
               

                // Run Maven on a Unix agent.
                sh "mvn test"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit 'target/surefire-reports/*.xml'
                    
                }
            }
        }
        stage('Package') {
            steps {
                // Get some code from a GitHub repository
                

                // Run Maven on a Unix agent.
                sh "mvn package"

                
            }
        }
        
    }
}
