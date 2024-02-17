pipeline {
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
    }
}
