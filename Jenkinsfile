pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        git(url: 'https://github.com/cicilymathew97/gitrepo2', branch: 'main', credentialsId: 'f260d02d-76c3-467f-b177-2315ff3470ce')
      }
    }

    stage('Build&Publish') {
      steps {
        sh '''sudo docker build -t cicilymathew97/srepo1:latest .
sudo docker push cicilymathew97/srepo1:latest'''
      }
    }

    stage('Deploy') {
      parallel {
        stage('DeployDev') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)||true
sudo docker run -d -p 7777:80 --name devcon1 cicilymathew97/srepo1:latest'''
          }
        }

        stage('DeployQA') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)||true
sudo docker run -d -p 9999:80 --name qacon1 cicilymathew97/srepo1:latest'''
          }
        }

      }
    }

  }
}