
pipeline {
    agent any
    environment {
    DOCKERHUB_CREDENTIALS = credentials('valaxy-dockerhub')
    }
    stages {
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/Anandcafex/nodejs-demos.git'
            }
        }

        stage('Build docker image') {
            steps {
                sh 'docker build -t node/nodejs-demos:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                withCredentials([usernamePassword(credentialsId: 'Dockerhub-credentials', passwordVariable: 'DOCKERHUB_CREDENTIALS_PSW', usernameVariable: 'DOCKERHUB_CREDENTIALS_USR')]) 
                sh 'echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push Anandcafex/nodejs-apps:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
