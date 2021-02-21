pipeline {

  environment {
    registry = "harbor.labs.local/tkr/webapl1"
    dockerImage = ""
  }

  agent any
  stages {
    stage("test") {
      steps {
              sh 'ls -al'
              sh 'env'
      }
    }

    stage('コンテナイメージのビルド') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
      
    stage('コンテナレジストリへプッシュ') {
      steps {
        script {
          docker.withRegistry("https://harbor.labs.local/tkr/","harborproj1") {
            dockerImage.push()
          }
        }
      }
    }
  }

}

