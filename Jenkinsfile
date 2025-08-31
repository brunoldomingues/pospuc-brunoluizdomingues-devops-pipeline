pipeline {
    agent any

    environment {
        IMAGE_WEB = "atividade02-web"
        IMAGE_DB = "atividade02-db"
    }

    stages {
        stage('Cleanup') {
            steps {
                echo "Limpando containers e imagens antigas..."
                sh 'docker-compose down -v || true'
                sh 'docker system prune -af || true'
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/brunoldomingues/pospuc-brunoluizdomingues-devops-pipeline.git'
            }
        }

        stage('Build') {
            steps {
                echo "Construindo imagens Docker..."
                sh 'docker-compose build'
            }
        }

        stage('Deploy') {
            steps {
                echo "Subindo containers..."
                sh 'docker-compose up -d'
            }
        }
    }
}
