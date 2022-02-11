pipeline {
  environment {
    imageName = 'hello'
    containerName = 'hello'
  }
  agent {
    label 'hello'
  }
  stages {
    stage('Build Jar') {
      steps {
        sh './gradlew clean build'
      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          docker.build(imageName)
        }
      }
    }

    stage('Docker Run') {
      steps {
        sh """
          docker stop ${containerName} && docker rm ${containerName}
          docker run -d --name ${containerName} -p 8080:8080 ${imageName}
        """
      }
    }
  }
}