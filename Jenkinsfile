pipeline {
agent any
  environment {
    //     AWS_ACCESS_KEY_ID = credentials('k8s deployment')
    //     AWS_SECRET_ACCESS_KEY = credentials('k8s deployment')
    // AWS_DEFAULT_REGION = "us-east-1"
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

   stage('Deploy to EKS') {
   // environment{
   //      // AWS_ACCESS_KEY_ID = credentials('k8s deployment')
   //      // AWS_SECRET_ACCESS_KEY = credentials('k8s deployment')
   //      // AWS_DEFAULT_REGION = "us-east-1"
   // }
     steps{
      sh 'kubectl apply -f deployment.yml'
    }
  }

  }

}
