pipeline {
    agent any
    stages
    {
        stage('Build Image in Docker') {
            steps {
                echo "Build Docker Image"
                bat "docker build -t kubdemoapp:v1 ."
            }
        }
        stage('Docker Login') {
            steps {
                echo "login into Docker"
                bat 'docker login -u eddulapreethi -p Epr_@2005'
            }
        }
        stage('pushing the Docker Image to Docker Hub') {
            steps {
                echo "push Image to Docker Hub"
                bat "docker tag kubdemoapp:v1 eddulapreethi/simple_demo:kubeimage1"               
                bat "docker push eddulapreethi/simple_demo:kubeimage1"
                
            }
        }
        stage('Kubernetes stage') { 
            steps { 
                    bat 'kubectl apply -f deployment.yaml --validate=false' 
                    bat 'kubectl apply -f service.yaml' 
            } 
        }
    }
    post {
        success {
            echo 'The execution is successful'
        }
        failure {
            echo 'There is a failure in pipeline'
        }
    }
}