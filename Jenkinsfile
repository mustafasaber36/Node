pipeline {

     
    agent any

    stages {
        stage('Fetching Code') {
            steps {
                
                git 'https://github.com/mustafasaber36/Node.git'
                sh 'pwd'
                sh 'ls'
            }
        }
        
        stage('Building Artifact'){
            steps{
               
                withCredentials([usernamePassword(credentialsId: 'dockerhubsecrets', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]){
                
                
                sh '''
                    docker build . -f dockerfile -t moustafasaber36/my-node-app:final
                    docker login -u ${USERNAME} -p ${PASSWORD}
                    docker push moustafasaber36/my-node-app:final
                '''
                }
            }   
        }

        stage('Deploying On GKE'){
            steps{
                    sh 'pwd'
                    sh 'ls'
                    
                    sh 'kubectl apply -f ~/workspace/cd/kuberneres/namespace.yml'
                    sh 'kubectl apply -f ~/workspace/cd/kuberneres/node-deploy.yml -n my-node-app' 
                    sh 'kubectl apply -f ~/workspace/cd/kuberneres/node-service.yml -n my-node-app'
             }
           }
    }
}
