pipeline {
agent any
  environment {
    AWS_ACCESS_KEY_ID = AKIAQUHKOX7KLWMOBOWH
    AWS_SECRET_ACCESS_KEY = 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
    AWS_DEFAULT_REGION = us-east-1
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
