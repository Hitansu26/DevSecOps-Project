pipeline{
    agent any
    tools {
        nodejs 'Nodejs_16'
    }
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }
    stages{
        stage("Clean Workspace"){
            steps{
                cleanWs()
            }
        }
        stage("Checkout From Git"){
            steps {
                git branch: 'main', url: 'https://github.com/Hitansu26/DevSecOps-Project.git'
            }
        }
        stage("Sonarqube Analysis"){
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Nteflix-Clone \
                    -Dsonar.projectKey=Nteflix-Clone'''
            }
        }
        }
        stage('QualityGate') {
            steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: '	SONAR_TOKEN'
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                sh "npm install"
            }
        }
        }
    }
  
