pipeline {
    agent any
    tools {
        maven 'Maven_'
        jdk 'JDK_'
    }
    environment {
	    APP_NAME = "register-app-pipeline"
            RELEASE = "1.0.0"
            DOCKER_USER = "thuyein97"
            DOCKER_PASS = 'dockerhub'
            IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
            IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
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
	stage("Build & Push Docker Image") {
            steps {
                script {
                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image = docker.build "${IMAGE_NAME}"
                    }

                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image.push("${IMAGE_TAG}")
                        docker_image.push('latest')
                    }
                }
            }

       }
    }
}
