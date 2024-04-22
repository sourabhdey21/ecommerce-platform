pipeline {
    agent any
    environment {
        DOCKER_CREDENTIALS = credentials('docker-credentials')
    }
    stages {
        stage('Build') {
            steps {
                sh 'cp -r ./* ./backup/' // Assuming copy.bat was meant to backup files. Adjust as necessary.
                sh 'docker build -t uc1 ./uc1'
                sh 'docker login -u ${rhea19} -p ${Rhea@1912} ${https://index.docker.io/v1/}'
                sh 'docker tag uc1 rhea19/uc1:latest'
                sh 'docker push rhea19/uc1:latest'
                sh 'docker build -t uc2 ./uc2'
                sh 'docker tag uc2 rhea19/uc2:latest'
                sh 'docker push rhea19/uc2:latest'
                sh 'docker build -t uc3 ./uc3'
                sh 'docker tag uc3 rhea19/uc3:latest'
                sh 'docker push rhea19/uc3:latest'
                sh 'docker build -t frontend ./frontend'
                sh 'docker tag frontend rhea19/frontend:latest'
            }
        }
        
        stage('Deploy') {
            steps {
                 sh 'kubectl apply -f kubernetes.yaml'
            }
        }
    }
    
    post {
        failure {
            echo 'Pipeline failed'
        }
    }
}
