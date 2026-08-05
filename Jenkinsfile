pipeline {
    environment {
        DOCKERHUB_CREDS = credentials('f784176f-4468-4d37-8966-056d4ac0bc6b')
    }
    agent {
        label 'K-M'
    }
    stages {
        stage('Git') {
            steps {
                git url: 'https://github.com/Naveen-86/Website-PRT-ORG' branch: 'main'
            }
        }
        stage('Docker') {
            steps {
                sh 'sudo docker login -u ${DOCKERHUB_CREDS_USR} -p ${DOCKERHUB_CREDS_PSW}'
                sh 'sudo docker build . -t naveen8698/prt-task'
                sh 'sudo docker push naveen8698/prt-task'
            }
        }

        stage('k8s'){
            steps {
               sh 'kubectl apply -f deploy.yaml'
               sh 'kubectl apply -f service.yaml'
         }
       }
    }
}
