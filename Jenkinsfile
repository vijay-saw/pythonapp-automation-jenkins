pipeline {

  agent any

  environment {
    IMAGE_TAG = "${BUILD_NUMBER}"
  }

  stages {
    stage('Checkout'){
      steps {
        git branch: 'main',
             url: 'https://github.com/vijay-saw/pythonapp-automation-jenkins.git'
      }
    }

    stage('Build Docker'){
      steps{
        script {
          sh '''
          echo 'Build Docker Image'
          docker build -t vijaysaw9211/todopythonpp:${BUILD_NUMBER} .
          '''
        }
      }
    }

    stage('Push the artifacts'){
      steps{
        script {
          sh '''
          echo 'Push to Repo'
          docker push abhishekf5/cicd-e2e:${BUILD_NUMBER}
          '''
        }
      }
    }

    stage('Checkout K8S manifest SCM'){
      steps {
        url: 'https://github.com/vijay-saw/pythonapp-automation-jenkins/tree/main/deploy',
          branch: 'main'
      }
    }
  }
}
