pipeline {
    agent {label 'Agent_VM' }
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
            setps {
                git branch: 'main', url: https://github.com/thuyein97/Jenkins_Project
            }
        }
        stage("Build and Test"){
            steps {
                sh "mvn clean package"
            }
        }
    }
}
