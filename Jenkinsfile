pipeline {
  agent any
  stages {
    stage('git pull') {
      steps {
        // Git-URL will replace by sed command before RUN
        git url: 'https://github.com/cresper/GitOps.git', branch: 'main'
      }
    }
    stage('k8s deploy'){
      steps {
        withCredentials([file(credentialsId: 'kubeconfig', variable: 'KUBECONFIG_FILE')]){
        //  kubernetesDeploy(kubeconfigId: 'kubeconfig',configs: '*.yaml')
          kubernetesDeploy(kubeconfig: readFile(KUBECONFIG_FILE), configs: '*.yaml')
        }
      }
    }
  }
}
