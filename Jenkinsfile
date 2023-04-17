pipeline {
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

    stage('Build') {
      steps {
        sh 'docker build -t alexander81/flask_app .'
      }
    }

    stage('Docker log in') {
      steps {
        sh 'docker login -u alexanderw81 -p dckr_pat_vMH9UBEAgzgY08Aa1yS20sUgocA'
      }
    }

    stage('Docker push') {
      steps {
        sh 'docker push alexanderw81/flask_app'
      }
    }

  }
}