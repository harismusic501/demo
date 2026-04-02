pipeline {
  agent any

  tools {
    maven 'Maven3'
  }

  environment {
    IMAGE_NAME = "springboot-app"
  }


  stages {

    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build JAR') {
      steps {
        sh 'mvn clean package'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t springboot-app:latest .'
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        sh 'kubectl apply -f k8s/'
        sh 'kubectl rollout restart deployment/springboot-app'
        sh 'kubectl rollout status deployment/springboot-app --timeout=120s'
      }
    }

  }
}