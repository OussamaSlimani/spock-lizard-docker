pipeline {
  agent any
  stages {
    stage('Log Tool Versions') {
      steps {
        parallel {
          stage('Log Maven Version') {
            steps {
              sh 'mvn --version'
            }
          }
          stage('Log Git Version') {
            steps {
              sh 'git --version'
            }
          }
          stage('Log Java Version') {
            steps {
              sh 'java -version'
            }
          }
        }
      }
    }

    stage('Build with Maven') {
      steps {
        sh 'mvn compile'
      }
    }

    stage('Run Tests') {
      steps {
        sh 'mvn test'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t oussamaslimani2001/cams-rps-service .'
      }
    }

    stage('Push Docker Image') {
      steps {
          sh 'docker push oussamaslimani2001/cams-rps-service:first'
      }
    }
  }

  post {
    always {
      cleanWs()
    }
    success {
      echo 'Build and deployment succeeded.'
    }
    failure {
      echo 'Build or deployment failed.'
    }
  }
}
