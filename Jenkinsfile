pipeline {
    agent {label  'dev-agent'}
    
    stages{
        stage('code'){
            steps {
                git url:'https://github.com/AkashBhadana/node-todo-cicd.git', branch: 'master'
            }
        }
       
       stage('build and test'){
            steps {
             sh 'docker build . -t boot83/node-todo-app:latest'
            }
        }
        stage('Logging and Pushing Image'){
            steps {
             echo 'login in to docker hub and pushing image..'
             withCredentials([usernamePassword(credentialsId:'dockerHub',passwordVariable:'dockerhubpassword', usernameVariable:'dockerhubuser')])
             {
                 sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpassword}"
                 sh "docker push boot83/node-todo-app:latest"
             }
            }
        }
        stage('Deploy'){
            steps {
               sh 'docker-compose down && docker-compose up -d'
            }
        }
    }

}
