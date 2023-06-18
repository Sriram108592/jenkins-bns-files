pipeline {
    agent any
    tools
    {
        maven 'maven'
    }
    stages {
        stage('maven build') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Sriram108592/hello-world.git']])
                sh 'mvn clean install'
            }
        }
        stage('Build Image and push') {
            steps {
                script{
                    sh 'docker build -t sriram108592/my-app:latest .'
                    withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                    sh 'docker login -u ${USERNAME} -p ${PASSWORD}'
                    }
                    sh 'docker push sriram108592/my-app:latest'
                }
            }
        }
    }
}
