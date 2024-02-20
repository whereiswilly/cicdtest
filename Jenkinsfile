pipeline {
  agent any
  stages {
    stage('git scm 업데이트') {
      steps {
        git url: 'https://github.com/whereiswilly/cicdtest.git', branch: 'main'
      }
    }
    stage('docker build and 푸쉬') {
      steps {
        sh '''
        docker build -t koreapower98/cicdtest:green .
        docker push koreapower98/cicdtest:green
        '''
      }
    }
    stage('deploy 쿠버네티스') {
      steps {
        sh '''
        ansible master -m command -a 'kubectl create deployment pipeline-deploy --image=koreapower98/cicdtest:green'
        ansible master -m command -a 'kubectl expose deployment pipeline-deploy --type=LoadBalanver --port=80 --target-port=80 --name=pipeline-deploy'

        '''
      }
    }
  }
}
