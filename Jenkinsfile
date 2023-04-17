pipeline {
  environment {
    registry = 'alexanderw81/flask_app'
    registryCredentials = 'docker'
    cluster_name = 'skillstorm'
  }
  agent {
    node {
      label 'docker'
    }

  }
  stages {
    stage('Git') {
      steps {
        git(branch: 'main', url: 'https://github.com/WAlexanderGA/flasky.git')
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
    }
  }

  
