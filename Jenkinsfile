pipeline {
agent any
  environment {
    //     AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
    //     AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
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

  // stage('Apply Kubernetes files') {
   // withKubeConfig([credentialsId: 'k8scred', serverUrl: 'https://172.31.15.134:6443']) {
      //sh 'kubectl apply -f deployment.yml'
    //}
  //}

  }

}
