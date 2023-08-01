pipeline {
    agent any
    tools{
        jdk  'jdk11'
        maven  'maven3'
        docker 'docker'
    }
    stages {
        stage('git checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ankushputtaswamy/Java-Project.git'
            }
        }
        
        stage('COMPILE') {
            steps {
                sh "mvn clean compile -DskipTests=true"
            }
        }   
        
        stage('Build') {
            steps {
                sh "mvn clean package -DskipTests=true"
            }
        }
        
        stage('Docker Build & Push') {
            steps {
                script{
                    withDockerRegistry(credentialsId: '89c6d379-af23-4049-97f7-88a1c145d5c9', toolName: 'docker', url: 'https://hub.docker.com/') {
                        
                        sh "docker build -t shopping-cart -f docker/Dockerfile ."
                        sh "docker tag  shopping-cart ankushputtaswamy/shopping-cart:latest"
                        sh "docker push ankushputtaswamy/shopping-cart:latest"
                    }
                }
            }
        }  
    }
}
