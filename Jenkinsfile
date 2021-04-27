pipeline {
  environment {
        registry = "diptibagal3010"
        dockerImage = ''
        Name = "my_image"
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/BagalDipti/Python_sqlite.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + "/" +Name+":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '' ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Docker Run') {
        steps {
          script {
             sh "docker rm Flask-app --force"
            dockerImage.run(" -p 7878:7878 --rm --name Flask-app")
          }
        }

    }

  }
}
