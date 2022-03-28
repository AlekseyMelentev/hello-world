pipeline {
  environment {
    imagename = "alekseymelentev/hello-world"
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/AlekseyMelentev/hello-world.git', branch: 'main'])
 
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
            docker.withRegistry( 'http://nexus.example.com:8283', 'nexus_creds' ) {
                dockerImage.push("$BUILD_NUMBER")
                dockerImage.push('latest')
            }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imagename:latest"
      }
    }
  }
}
