pipeline {
    agent none

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "mymaven"
    }
    parameters{
        string(name:'Env', defaultValue:'Test',description:'Environment to deploy')
        booleanParam(name:'executeTests', defaultValue:true, description:'Whether to run or not')
        choice(name:'AppVersion',choices:['1','2','3'])
    }

    stages {
        stage('compile') {
            agent any
            steps {
                git 'https://github.com/Pavanmeesi/addressbook.git'
                sh "mvn compile"
            }
        }
        stage('UnitTest') {
            agent any
            when{
                expression{
                    params.executeTests == true
                }
            }
            steps {
                sh "mvn test"
            }
            post {
                success {
                    junit 'target/surefire-reports/*.xml'    
                }
            }
        }
        stage('Package') {
            agent{label:'linux_slave'}
            steps {
                sh "mvn package"
                echo "deploying the app version: ${params.AppVersion}"
                
            }
        }
        stage('Deploy'){
            agent{label:'linux_slave'}
            steps{
                input{
                    message: "Please provide the approval"
                    ok "Yes to deploy"
                    parameters{
                        choices:{name:'AppVersion',choice['1.1','1.2']}
                    }
                }
            }
        }
        
    }
}
