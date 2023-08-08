pipeline {
agent any
  environment {

    dockerimagename = "tejendranaidu/demo"
    dockerImage = ""
  }



  stages {

    stage('Checkout Source') {
      
      steps {
       
        git 'https://github.com/TEJA176/nodeapp_test.git'
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
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }

    stage('Deploying App to Kubernetes') {
      steps {
        script {
          sh 'kubectl apply -f deployment.yml'
        }
      }
    }

  }

}
