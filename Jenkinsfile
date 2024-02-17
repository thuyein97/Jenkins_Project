erpipeline {
    agent any
    tools {
        maven 'Maven_'
        jdk 'JDK_'
    }
    stages {
        stage("Starting CI"){
            steps {
                cleanWs()
            }
        }
        stage("Checkout Git"){
            steps {
                script {
                    git branch: 'main',
                        url: 'https://github.com/thuyein97/Jenkins_Project'
                }
            }
        }
        stage("Build and Test"){
            steps {
                sh "mvn clean package"
            }
        }
        stage('SonarQube analysis') {
            withSonarQubeEnv(credentialsId: 'ace76f06-b6d9-4692-bb6c-05391c25110f', installationName: 'sonarqube-server') { // You can override the credential to be used
                sh 'mvn sonar:sonar'
            }
        }
    }
}
