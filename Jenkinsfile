pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'git@github.com:Feruza-M/java-docker-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t java-docker-app .'
            }
        }

        stage('Run Container') {
            steps {
                // Убираем старый контейнер, если есть
                sh 'docker rm -f java-docker-app || true'
                sh 'docker run -d -p 8080:8080 --name java-docker-app java-docker-app'
            }
        }
    }
}
