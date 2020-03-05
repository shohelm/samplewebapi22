pipeline {

  environment {
    registry = "10.16.131.56:5000/samplewebapi"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/shohelm/samplewebapi22.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":latest"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "" ) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Deploy App') {
      steps {
        script {
		 kubernetesDeploy(configs: "SampleWebApi/samplewebapi-deployment.yml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
