pipeline {
    agent { label 'dev-agent' }
    stages {
        stage("code")
        {
            steps {
                git url: 'https://github.com/bagnedinesh/node-todo-cicd.git', branch: 'master'
            }
        }
         stage("build")
        {
            steps {
                sh 'docker build . -t dineshbagne/node-todo-app:latest'
            }
        }
         stage("login and push image")
        {
            steps {
                echo "login into docker hub and push the image"
                withCredentials([usernamePassword(credentialsId:'dockerhub',passwordVariable:'dockerhubPassword',usernameVariable:'dockerhubUser')])
                {
                    sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPassword}"
                    sh "docker push dineshbagne/node-todo-app:latest"
                }
            }
        }
         stage("deployed")
        {
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
