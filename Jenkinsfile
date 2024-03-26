pipeline {
    agent any
    tools {
        maven 'Maven.3.9.6'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/OsheaReid/devops-inte.git']])
                bat 'mvn clean install'
            }
        }
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t osheareid8080/devops-integration .'
            }
        } 
        
        stage('Push Image to Hub') {
            steps {
               withCredentials([string(credentialsId: 'lab3docker', variable: 'dockerpass')]) {
                    bat 'echo %dockerpass% | docker login -u osheareid8080 --password-stdin'
                }
                
                bat 'docker push osheareid8080/devops-integration:latest'
            }
        }
    }
}
