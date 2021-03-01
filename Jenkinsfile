pipeline {
   
 environment { 
   
    registry = "shooxep0daemon/boxfuse" 
    registryCredential = '78ee7a22-77d0-4ccc-b599-65c0d5541d19' 
    dockerImage = 'shooxep0daemon/boxfuse:latest' 

    }

  agent any

  stages {
    stage('Clone github repo') {
      steps {
        //get git repo from scm addr
        checkout scm
            }
    }

    stage('Build docker image') {
      steps {
        // build from dockerfile
        script {
            dockerImage = docker.build("$registry")
            }
           
    }}

    stage('Push image to DH') {
      steps {
           script {
                docker.withRegistry( '', registryCredential ) { 
                dockerImage.push() 
                }
        }
    }
    }

    stage('Pull and RUN image from DH') {
      steps {
           script {
                docker.image('$dockerImage').run() { 
                }
        }
    }
    }
  }
}
