pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Pegando código do GitHub...'
                checkout scm
            }
        }

        stage('Build Docker Images') {
            steps {
                echo 'Construindo imagens Docker...'
                sh 'docker build -t atividade02-db ./db'
                sh 'docker build -t atividade02-web ./web'
            }
        }

        stage('Run Containers') {
            steps {
                echo 'Subindo containers...'
                sh 'docker network create devops_net || true'
                sh 'docker run -d --name mysql_devops --network devops_net -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=docker_e_kubernetes -e MYSQL_USER=bruno -e MYSQL_PASSWORD=bruno123 atividade02-db'
                sh 'docker run -d --name flask_devops --network devops_net -p 8300:8300 -e MYSQL_USERNAME=bruno -e MYSQL_PASSWORD=bruno123 -e MYSQL_ADDRESS=mysql_devops:3306 -e MYSQL_DBNAME=docker_e_kubernetes atividade02-web'
            }
        }
    }
}

