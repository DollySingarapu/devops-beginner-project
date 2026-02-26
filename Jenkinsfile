pipeline {
  agent any

  stages {
    stage('Clone') {
      steps {
        git 'https://github.com/DollySingarapu/devops-beginner-project.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t devops-app .'
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        sh 'kubectl apply -f deployment.yaml'
        sh 'kubectl apply -f service.yaml'
      }
    }
  }
}
