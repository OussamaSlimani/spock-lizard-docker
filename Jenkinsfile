pipeline {
  agent any
  stages {
    stage('Log Tool Version') {
      parallel {
        stage('Log Tool Version') {
          steps {
            sh '''
              mvn --version
              git --version
              java -version
            '''
          }
        }

        stage('Check for POM') {
          steps {
            script {
              if (!fileExists('pom.xml')) {
                error 'pom.xml not found!'
              }
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

    stage('Run Static Code Analysis') {
      steps {
        build job: 'static-code-analysis'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'sudo docker build -t cameronmcnz/cams-rps-service .'
      }
    }

    stage('Create Executable JAR File') {
      steps {
        sh 'mvn package spring-boot:repackage'
      }
    }

    stage('Push Docker Image') {
      steps {
        sh 'docker push cameronmcnz/cams-rps-service:first'
      }
    }
  }
}
