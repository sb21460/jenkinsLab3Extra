pipeline{
    agent any
    stages{
        stage("cleanup"){
            steps{
                sh 'docker rm -f $(docker ps -a -q) || true'
                sh 'docker network create new-network || true'
            }
        }
        stage("build"){
            steps{
                sh 'docker build -t nginx-image -f Dockerfile.nginx .'
                sh 'docker build -t flask-app-image .'
            }
        }
        stage("run"){
            steps{
                sh 'docker run -d --network new-network --name flask-app flask-app-image'
                sh 'docker run -d --network new-network -p 80:80 --name nginx-container nginx-image'
                
            }
        }
        stage("test"){
            steps{
                sh 'curl localhost'
                
            }
        }
    }
