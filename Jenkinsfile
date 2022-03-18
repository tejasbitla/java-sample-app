pipeline{
    agent any
    stages{
        stage("CheckoutStage"){
            steps{
               checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'crazy4devops-jenkins-github-token', url: 'https://github.com/crazy4devops/java-sample-app.git']]])
            }
        }
        stage("Build Source Code"){
            steps{
                echo "Building Source Code"
            
            }
        }

        stage("Run UNIT-Tests"){
            steps{
                echo "Runnning Unit Tests"
              
            }
        }

        stage("Static Code Analysis"){
            steps{
                echo "Runnning Code Analysis"
            
            }
        }
    }
}
