pipeline {
    agent any

    stages {
        stage('Cleanup') {
            steps {
                echo 'Limpando workspace e containers não finalizados'
                sh 'docker system prune -f || true'
            }
        }

        stage('Checkout') {
            steps {
                echo 'Fazendo checkout do código'
                checkout scm
            }
        }

        stage('Construção') {
            steps {
                echo 'Construindo imagens Docker'
                sh 'docker compose build'
            }
        }

        stage('Entrega') {
            steps {
                echo 'Subindo containers'
                sh 'docker compose up -d'
            }
        }
    }

    post {
        success {
            echo 'Pipeline finalizada com sucesso!'
        }
        failure {
            echo 'Pipeline falhou!'
        }
    }
}