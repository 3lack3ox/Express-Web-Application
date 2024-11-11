pipeline {
  agent any

  stages {
    stage('Clone Repository') {
      steps {
        git branch: 'main', url: 'https://github.com/3lack3ox/Express-Web-Application'
      }
    }
    stage('Build Docker Image') {
      steps {
        script {
          dockerImage = docker.build('my-node-website')
        }
      }
    }
    stage('Run Tests') {
      steps {
        script {
          // Run tests within the Docker container using the built image
          dockerImage.run('-t --rm my-node-website npm test')
        }
      }
    }
    stage('Deploy') {
      steps {
        script {
          sh 'docker stop my-node-website || true && docker rm my-node-website || true'
          sh 'docker run -d -p 8080:3000 --name my-node-website my-node-website'
        }
      }
    }
  }
}
