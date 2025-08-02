pipeline {
  agent any

  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub-login')
  }

  stages {
    stage('Clone Repo') {
      steps {
         git branch: 'main', url: 'https://github.com/Seetharamj/Devops-project-.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        dir('app') {
          sh 'docker build -t seetharam10/devops-node-app .'
        }
      }
    }

    stage('Push to DockerHub') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
        sh 'docker push seetharam10/devops-node-app'
      }
    }

    stage('Deploy to EC2') {
      steps {
        sshagent(['ec2-ssh-key']) {
          sh '''
            ssh -o StrictHostKeyChecking=no ubuntu@13.201.127.123 '
              docker pull seetharam10/devops-node-app &&
              docker stop devops-app || true &&
              docker rm devops-app || true &&
              docker run -d -p 3000:3000 --name devops-app seetharam10/devops-node-app
            '
          '''
        }
      }
    }
  }

  post {
    success {
      echo '✅ Pipeline completed successfully!'
    }
    failure {
      echo '❌ Pipeline failed. Check the logs above.'
    }
  }
}
