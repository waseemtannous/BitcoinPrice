pipeline {

  agent any

  stages {
    stage('Build Image') {
      steps {
        sh 'docker build -t bitcoin-price .'
      }
    }

    stage('Push Image') {
      steps {
        sh 'docker tag bitcoin-price waseemtannous/bitcoin-price:latest'
        sh 'docker push waseemtannous/bitcoin-price:latest'
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