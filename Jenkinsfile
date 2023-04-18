pipeline {
  environment {
    registry = 'alexanderw81/flask_app'
    registryCredentials = 'docker'
    cluster_name = 'skillstorm'
    namespace = 'alexanderw81'
  }
  agent {
    node {
      label 'docker'
    }

  }
  stages {
    stage('Git') {
      steps {
        git(branch: 'main', url: 'https://github.com/WAlexanderGA/flask.git')
      }
    }

stage('Build Stage') {
    steps{
      script {
        dockerImage = docker.build(registry)
      }
     }
    }
stage('Deploy Stage') {
    steps {
        script {
           docker.withRegistry('', registryCredentials) {
                dockerImage.push()
            }
          }
        }
      }
stage('Kubernetes') {
  steps {
    withCredentials([aws(accessKeyVariable: 'AWS_ACCESS_KEY_ID', CredentialsId:
    'AWM_SECRECT_ACCESS_KEY')]) {
      sh "aws eks update-kubeconfig --region us-east-1 --name ${cluster_name}"
      script{
        try{
          sh "kubectl create namespace ${namespace}"
        }catch (Exception e) {
            echo "Exception handled"
        }
        }
      sh "kubectl apply -f deployment.yaml in ${namespace}"
      sh "kubectl -n ${namespace} rollout restart deployment flaskcontainer"
        }
      }
    }
  }
}
    
  

  