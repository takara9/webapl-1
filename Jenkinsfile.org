pipeline {

  environment {
    registry = "harbor.labs.local/tkr/webapl1"
    dockerImage = ""
    KUBECONFIG = credentials('kubeconfig')
  }

  agent any
  stages {
    stage("gitlabからのクローン") {
      steps {
        checkout([$class: 'GitSCM',
                 branches: [[name: '*/master' ]],
                 extensions: scm.extensions,
                 userRemoteConfigs: [[
                   url: "$GIT_URL",
                   credentialsId: 'gitlab-sshkey2'
                 ]]
        ])
      }
    }
      
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
      
    stage('K8sクラスタへのデプロイ') {
      steps {
        script {
          sh 'kubectl cluster-info --kubeconfig $KUBECONFIG'
          sh 'sed s/__BUILDNUMBER__/$BUILD_NUMBER/ myweb.yaml > deploy_myweb.yaml'
          sh 'kubectl apply -f deploy_myweb.yaml --kubeconfig $KUBECONFIG'
        }
      }
    }
  }

}

