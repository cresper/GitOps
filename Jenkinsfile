pipeline {
  agent{
    kubernetes {
      inheritFrom 'default'
    }
    // label 'jenkins-jenkins-slave'
  }
  stages {
    stage('git pull') {
      steps {
        // Git-URL will replace by sed command before RUN
        git url: 'https://github.com/cresper/GitOps.git', branch: 'main'
      }
    }
    stage('k8s deploy') {
      steps {
        // Groovy Pipeline 스텝으로 withCredentials를 사용합니다.
        withCredentials([file(credentialsId: 'kubeconfig-file', variable: 'KUBECONFIG_FILE')]) {
          // withCredentials 블록 내에서 Shell 명령을 실행합니다.
          sh '''
            # $KUBECONFIG_FILE 변수는 withCredentials 스텝에 의해 이 쉘에 주입됩니다.
            kubectl apply --kubeconfig=$KUBECONFIG_FILE -f *.yaml
          '''
        }
      }
    }    
  }
}
