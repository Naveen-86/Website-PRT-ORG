pipeline {
    environment {
        DOCKERHUB_CREDS = credentials('4b19f7ef-3cc4-4d42-99ea-6264cc66592e')
    }
    agent any
    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-creds',
                    url: 'https://github.com/Naveen-86/Website-PRT-ORG'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t naveen8698/prt-task .'
            }
        }
        stage('Docker Login') {
            steps {
                sh "docker login -u ${DOCKERHUB_CREDS_USR} -p ${DOCKERHUB_CREDS_PSW}"
            }
        }
        stage('Push Docker Image') {
            steps {
                sh 'docker push naveen8698/prt-task'
            }
        }
        stage('Deploy To Kubernetes') {
            steps {
                sh 'kubectl apply -f deploy.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }
    }
}
