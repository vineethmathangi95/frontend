pipeline {
      agent any
      stages {
         stage ('Build') {
          steps {
             sh '''cd $WORKSPACE
                   docker build -t devops-react:v${BUILD_NUMBER} .'''
             }
           }
           stage('docker login ') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                }
            }
        }

        stage('docker tagging ') {
            steps {
                sh 'docker tag frontend:v${BUILD_NUMBER} vineethmathangi95/threetier:reactjs-v${BUILD_NUMBER}'
            }
        }

        stage('image push dockerhub ') {
            steps {
                sh 'docker push vineethmathangi95/threetier:reactjs-v${BUILD_NUMBER}'
            }
        }
          }
        }
