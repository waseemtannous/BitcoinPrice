pipeline {

  agent any

  stages {
    stage('Build Image') {
      steps {
        sh 'whoami'
        sh 'docker build -t bitcoin-price .'
      }
    }

    stage('Push Image') {
      steps {
        withCredentials([string(credentialsId: 'DockerSecret', variable: 'TOKEN')]) {
            sh 'docker login -u waseemtannous -p ${TOKEN}'
            sh 'docker tag bitcoin-price waseemtannous/bitcoin-price:latest'
            sh 'docker push waseemtannous/bitcoin-price:latest'
        }
      }
    }
  }

  post {
      failure {
        script {
          slackSend(
            color: "#FF0000",
            channel: "personal-projects",
            message: "Bitcoin-Price Status: FAILED"
          )
        }
      }

     success {
        script {
          slackSend(
            color: "#00FF00",
            channel: "personal-projects",
            message: "Bitcoin-Price Status: SUCCESS"
          )
        }
      }
    }
}