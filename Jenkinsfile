pipeline {
  agent any

  environment {
    IMAGE_NAME = "springboot-app"
  }


  tools {
      maven 'M3' // This name must match the name in Global Tool Configuration
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
      }
    }

  }
}