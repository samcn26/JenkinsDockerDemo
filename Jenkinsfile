pipeline {
    agent any

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
                sh "echo ${env.DOCKER_PASSWORD} | docker login --username ${env.DOCKER_USERNAME} --password-stdin"
                sh "docker push samcn26/tomcatwebapp:${env.BUILD_NUMBER}"                    
            }
        }
    }
}