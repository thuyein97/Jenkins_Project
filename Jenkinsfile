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
        stage("Build Application"){
            steps {
                sh "mvn clean package"
            }
        }
        stage("SonarQube Analysis"){
           steps {
	           script {
		            withSonarQubeEnv(credentialsId: 'ace76f06-b6d9-4692-bb6c-05391c25110f') { 
                    sh "mvn sonar:sonar"
		            }
	           }	
           }
       }
	stage("Quality Gate"){
	    steps {
		    script {
                    	waitForQualityGate abortPipeline: false, credentialsId: 'ace76f06-b6d9-4692-bb6c-05391c25110f'
                    }
	    }
	}
    }
}
