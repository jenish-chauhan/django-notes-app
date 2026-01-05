@Library('Shared') _
pipeline {
    agent {
        label 'node-1'
    }

    environment {
        IMAGE_NAME = "django-notes-app"
        CONTAINER_NAME = "django-app"
    }

    stages {

        stage('Clone Code') {
            steps {
                script {
                    gitclone(
                        'https://github.com/jenish-chauhan/django-notes-app.git',
                        'main'
                    )
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    buildDockerImage('$IMAGE_NAME')
                }
            }
        }
          stage('Run Container') {
             steps {
                 script{
                    runContainer(
                     '$IMAGE_NAME',
                     '$CONTAINER_NAME',
                     "8000:8000"
                     )   
                  }
                }
          }
          stage('push to the docker hub'){
            steps{
               script{
                   pushDockerHub('$IMAGE_NAME','dockerHubCred')
               }
            }
        }

        
    }
}
