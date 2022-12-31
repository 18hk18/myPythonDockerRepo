pipeline {
    agent any
        environment {
        //once you sign up for Docker hub, use that user_id here
        registry = "214577799134.dkr.ecr.us-east-1.amazonaws.com/springboot"
        //- update your credentials ID after creating credentials for connecting to Docker Hub
        registryCredential = 'aws'
        dockerImage = ''
    }
    stages 
    {

        stage ('checkout') {
            steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/developer']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/18hk18/myPythonDockerRepo']]])
            }
        }
       
        stage ('Build docker image') {
            steps {
                script {
                dockerImage = docker.build registry + ":$BUILD_NUMBER"
                //dockerImage = docker.build registry + ":$BUILD_NUMBER"

                }
            }
        }
       
         // Uploading Docker images into Docker Hub
    stage('Upload Image') {
     steps{   
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
            }
        }
      }
    }
  }  
}
