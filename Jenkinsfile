pipeline {
  agent any
  stages {
    stage('Log Tool Version') {
      parallel {
        stage('Log Tool Version') {
          steps {
            bat '''mvn --version
            git --version
            java -version'''
          }
        }

        stage('Check for POM') {
          steps {
            fileExists 'pom.xml'
          }
        }

      }
    }

    stage('Build with Maven') {
      steps {
        bat 'mvn compile'
      }
    }

    stage('Run Tests') {
      steps {
        bat 'mvn compile'
      }
    }

    stage('Run Static Code Analysis') {
      steps {
        build job: static-code-analysis
      }
    }

  

    stage('Build Docker Image') {
      steps {
        build job: static-code-analysis
      }
    }

    stage('Create Executable JAR File') {
      steps {
        bat 'mvn package spring-boot:repackage'
      }
    }  

    stage('Build Docker IMage') {
      steps {
        bat 'sudo docker build -t cameronmcnz/cams-rps-service .'
      }
    }   

    stage('Software Versions') {
            steps {
                        docker push cameronmcnz90210/cams-rps-service:first
                    
                }
            }
        }

  }
}
