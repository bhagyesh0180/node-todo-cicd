pipeline {
    agent { label 'dev'}
    stages{
        stage('code'){
            steps{
                git url : 'https://github.com/bhagyesh0180/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('build and test'){
            steps{
                sh 'docker build . -t bhagyesh0180/node-todo-new:latest'
            }
        }
        stage('docker login and push image'){
            steps{
                withCredentials([usernamePassword(credentialsId:'dockerHub',passwordVariable:'dockerHubPassword',usernameVariable:'dockerHubUser')]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                sh "docker push ${env.dockerHubUser}/node-todo-new:latest "
                }
            }
        }
        stage("deploy"){
            steps{
                sh 'docker-compose down'
                sh 'docker-compose up -d --no-deps --build web '
            }
        }    
    }
}    
