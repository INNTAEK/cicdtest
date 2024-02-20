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
        ansible master -m command -a 'kubectl create deployment pl-bulk-prod --image=inntaek/cicdtest:red'
        ansible master -m command -a 'kubectl expose deployment pl-bulk-prod --type=LoadBalancer --port=80 --target-port=80 --name=pl-bulk-prod-'

        '''
      }
    }
  }
}
