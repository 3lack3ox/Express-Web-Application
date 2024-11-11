pipeline {
  agent any

  environment {
    MONGODB_URI = mongodb+srv://Jason:3lack3ox@express.hsxg7fd.mongodb.net/express
  }

  stages {
    stage('Clone Repository') {
      steps {
        git branch: 'main', url: 'https://github.com/3lack3ox/Express-Web-Application'
      }
    }
    stage('Build Docker Image') {
      steps {
        script {
          sh 'docker-compose build'
        }
      }
    }
    stage('Deploy') {
      steps {
        script {
          // Make sure Docker Compose is installed on the Jenkins agent
          sh 'docker-compose up -d'
        }
      }
    }
    stage('Run Tests') {
      steps {
        script {
          sh 'docker-compose exec web npm test'
        }
      }
    }
  }
}
