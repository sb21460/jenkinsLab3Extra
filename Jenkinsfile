pipeline{
    agent any
    stages{
        stage("docker clean up"){
            steps{
                sh docker rm -f $(docker ps -a -q) || true
            }
        }
        stage("docker build"){
            steps{
                sh docker build -t flask-app:latest .
            }
        }
        stage("docker run"){
            steps{
                sh docker run -d \
                  --name flask-app \
                  -p 5500:80 \
                  flask-app:latest
            }
        }
    }
}
