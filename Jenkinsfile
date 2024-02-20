pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/INNTAEK/cicdtest.git', branch: 'main'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t inntaek/cicdtest:red .
        sudo docker push inntaek/cicdtest:red
        '''
      }
    }
    stage('deploy kubernetes') {
      steps {
        sh '''
        kubectl create deployment pl-bulk-prod --image=inntaek/cicdtest:red
        kubectl create deployment pl-bulk-prod --type=LoadBalanver --port=80 --target-port=80 --name=pl-bulk-prod-

        '''
      }
    }
  }
}
