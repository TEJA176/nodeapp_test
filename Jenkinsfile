pipeline {

  environment {

    dockerimagename = "tejendranadu/nodeapp"
    dockerImage = ""
  }

 agent none

  stages {

    stage('Checkout Source') {
       node('Jenkins-new-slave-java11-8084')
      steps {
        node('Jenkins-new-slave-java11-8084'){
        git 'https://github.com/TEJA176/nodeapp_test.git'
      }
    }
    }
    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'dockerhublogin'
           }
      steps{
        script {
          docker.withRegistry( 'https://hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
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
