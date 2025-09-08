pipeline {
    agent any

    environment {
        // variaveis de ambiente
        GITHUB_TOKEN = credentials('github-pat')
    }

    stages{
        stage('Cleanup') {
            steps {
                echo 'Limpando workspace...'

                deleteDir()
            }
        }

        stage('Checkout') {
            steps {
                echo 'Clonando repositório...'

                git branch: 'main',
                url: 'https://github.com/brunoldomingues/pospuc-brunoluizdomingues-devops-pipeline.git',
                credentialsId: 'github-pat'
            }
        }

        stage('Construção') {
            steps{
                echo 'Construindo imagens...'
                
                sh 'docker build --nochache -t atividade02-db ./db'
                sh 'docker build --nocache -t atividade02-web ./web'
            }
        }

        stage('Entrega') {
            steps {
                echo 'Rodando containers...'

                sh 'docker run -d --name atividade02-db -e MYSQL_ROOT_PASSWORD=root atividade02-db'
                sh 'docker run -d --name atividade02-web -p 8200:8200 --link atividade02-db:db -e MYSQL_USERNAME=root -e MYSQL_PASSWORD=root -e MYSQL_ADDRESS=db -e MYSQL_DBNAME=docker_e_kubernetes atividade02-web'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finalizada com sucesso'
        }
    }
}
