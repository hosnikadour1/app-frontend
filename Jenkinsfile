pipeline {
     environment {
    imagename = "hosnikadour/ites-app"
    registryCredential = 'dockerhub-devops'
    dockerImage = ''
  }

    agent any
    stages {
         stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/hosnikadour1/ITESLAB-app-reactjs-nodejs-frontend-backend.git', branch: 'main', credentialsId: 'github'])
 
      }
    }

        stage('Tests') {
            steps {
//                 script {
//                    docker.image('node:16-stretch').inside { c ->
                        echo 'Building..'
                        sh 'npm install'
                        echo 'Testing..'
                        sh 'npm test'
//                         sh "docker logs ${c.id}"
//                    }
//                 }
            }
        }
       


        
        stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }
    
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')  
            
        }
        }
        }
        }
stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imagename:$BUILD_NUMBER"
         sh "docker rmi $imagename:latest"

      }
    }
    
  }
}
        
         
    



         
 