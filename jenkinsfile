pipeline{
    agent any
    stages{
        stage('checkout code'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/bvenkydevops/Node_js_Project']])
            }
        }
        stage('Build docker image'){
            steps{
             script{
                 sh 'docker build -t images:2.0 .'
             }   
            }
        }
        stage('create docker container'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]){
                        sh 'docker login -u bojjavenkatesh -p ${dockerhub}'
                    }
                       sh 'docker tag images:2.0 bojjavenkatesh/nodejs:2.0'
                       sh 'docker push bojjavenkatesh/nodejs:2.0'
                       sh 'docker container run -d -p 3000:3000 images:2.0 npm run start'
                }
            }
        }
    }
}
