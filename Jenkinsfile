pipeline {
    agent { label 'nodejs'}
    environment {
        DOCKERHUB_CREDENTIALS = credentials()
    }
    stages {
        // Fetch code from  github  
        stage('checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Sinjith-Reddy/express.git'
            }
        }
        // Build application
        stage('Build'){
            steps{
                sh 'npm install'
            }
        }
        // build docker image
        stage('Build Docker Image'){
            steps {
            sh 'docker build -t hello-world-expressjs:latest .'
            sh 'docker tag Hello-world-expressJs sinjithreddy/hello-world-expressjs:latest'
            }
        }
        //Login and Push image to DockerHub 
        stage ('Login to DockerHub'){
            steps {
                sh  'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        
        stage('Push image to DockerHub'){
            steps{
                sh 'docker push sinjithreddy/hello-world-expressjs:latest'
            }
        }
        post {
            always {
                sh 'docker logout'
            }
        }
        //deploy docker image
    }
}
