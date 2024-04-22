pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/sourabhdey21/ecommerce-platform'
            }
        }
        stage('Deploy') {
            steps {
                sh 'kubectl  apply  -f Db/mongo.yaml kubernetes.yaml'
            }
        }
    }
    post {
        success {
            echo 'Deployment successful'
        }
        failure {
            echo 'Deployment failed'
        }
    }
}
