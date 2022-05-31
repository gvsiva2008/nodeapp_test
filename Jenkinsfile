pipeline {

  environment {
    dockerimagename = "gvsiva2008/nodeapp"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/gvsiva2008/nodeapp_test.git'
      }
    }

    stage('Build image') {
      steps{
        script {
        sh "docker build -t <dockerhub_repo>/nodeapp ."
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'Dockerlogin'
           }
      steps{
         sh "docker login -u  -p "
         sh "docker push <dockerhub_repo>/nodeapp"
      }
    }

    stage('Deploying App to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deploymentservice.yml", kubeconfigId: "kubernetes")
        }
      }
    }

  }

}
