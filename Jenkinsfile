pipeline {
  agent any

  stages {
    stage('Clone Repo') {
      steps {
        git branch: 'main', url: 'https://github.com/Seetharamj/Devops-project-.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t seetharamj/devops-node-app .'
      }
    }

    stage('Push to DockerHub') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-login', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
          sh '''
            echo $PASSWORD | docker login -u $USERNAME --password-stdin
            docker push seetharamj/devops-node-app
          '''
        }
      }
    }

    stage('Deploy to EC2') {
      steps {
        sshagent(credentials: ['ec2-ssh-key']) {
          sh '''
            ssh -o StrictHostKeyChecking=no ubuntu@13.201.127.123 '
              docker pull seetharamj/devops-node-app &&
              docker stop devops-app || true &&
              docker rm devops-app || true &&
              docker run -d -p 3000:3000 --name devops-app seetharamj/devops-node-app
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
