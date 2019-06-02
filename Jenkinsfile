pipeline {
    agent any

    environment {
        DOCKERHUB = credentials ('dockerhub')
    }

    tools {
        maven 'localMaven'
    }

    stages {
        stage ('Build') {
            steps {
                sh 'mvn clean package'
                sh "docker build . -t samcn26/tomcatwebapp:${env.BUILD_NUMBER}"
            }
            post {
                success {
                   echo 'build success'
                }
            }
        }

        stage ('Push to docker hub') {
             steps {
                sh "echo ${DOCKERHUB_PSW} | docker login --username ${DOCKERHUB_USR} --password-stdin"
                sh "docker push samcn26/tomcatwebapp:${env.BUILD_NUMBER}"                    
            }
        }
    }
}