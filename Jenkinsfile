pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub-login')
  }

  stages {
    stage('Clone Repo') {
      steps {
        git 'https://github.com/your-user/your-repo.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t MyImage/nodeapp .'
      }
    }

    stage('Push to DockerHub') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
        sh 'docker push MyImage/nodeapp'
      }
    }

    stage('Deploy to EC2') {
      steps {
        sshagent(['ec2-ssh-key']) {
          sh '''
            ssh -o StrictHostKeyChecking=no ubuntu@<APP_EC2_IP> '
              docker pull yourname/nodeapp &&
              docker stop nodeapp || true &&
              docker rm nodeapp || true &&
              docker run -d -p 3000:3000 --name nodeapp yourname/nodeapp
            '
          '''
        }
      }
    }
  }
}
