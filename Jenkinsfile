pipeline {
    agent any
    environment {
        git_repo_url = "https://github.com/crazy4devops/java-sample-app.git"
        git_repo_br = "feature/batch-II"
    }
    stages{
        stage("Checkout"){
            steps {
                // Clean before build
                cleanWs()
                git url: "${git_repo_url}", branch: "${git_repo_br}"
            }
        }
        stage("Build Source Code"){
            steps {
                    sh "mvn install"
                    sh "mv target/jb-hello-world*.jar target/demoApp-${BUILD_NUMBER}.jar"
            }
        }
        stage("Run Unit-Tests"){
            steps {
                    sh "mvn test"
            }
        }
        stage('Sonarqube Analysis') {
            environment {
              def scannerHome = tool 'SonarQubeScanner'
            }
            steps {  
                withSonarQubeEnv('sonarserver') {
                    sh "/opt/sonar/bin/sonar-scanner"
                }
                sleep time: 30000, unit: 'MILLISECONDS'
                script {
                        def qg = waitForQualityGate()
                        if (qg.status != 'OK') {
                            error "Pipeline aborted due to quality gate failure: ${qg.status}"
                        }
                }
            }
        }
        stage("Upload Artifacts"){
            steps{
                rtUpload (
                    serverId: 'jfrog-server',
                    spec: '''{
                        "files": [
                            {
                            "pattern": "target/*.jar",
                            "target": "dummyrepo/demoApp/"
                            }
                        ]
                    }''',
                )
                    
            }
        }            
        stage("Deploy - DEV"){
            steps{
                echo "Running Deployment on Dev"
            }
        }  
        
        stage("Deploy - UAT"){
            steps{
                echo "Running Deployment on UAT"
            }
        }
        stage("Deploy - PRD"){
            steps{
                echo "Running Deployment on PRD"
            }
        } 
    
    }
}
