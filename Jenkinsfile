pipeline {
    agent any
    parameters {
        choices (name: 'APP', choices: ['java-app', 'python-app', 'ruby-app']),
        string(name: 'EXT_PORT', defaultValue: '5000'),
        string(name: 'INT_PORT', defaultValue: '5000')
    }

    environment {
        REPO = 'anestesia01/filiz-docker-apps',
        DOCKER_TOKEN = credentials('docker_token')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'git@github.com:AnastasiyaGapochkina01/java-docker-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${REPO}:${params.APP}-${BUILD_ID} ./${params.APP}'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh """
                  docker login -u anestesia01 -p ${DOCKER_TOKEN}
                  docker push ${REPO}:${params.APP}-${BUILD_ID}'
                """
            }
        }

        stage('Run Container') {
            steps {
                // Убираем старый контейнер, если есть
                sh 'docker rm -f ${params.APP}-cont || true'
                sh 'docker run -d -p ${EXT_PORT}:${INT_PORT} --name ${params.APP}-cont ${REPO}:${params.APP}-${BUILD_ID}'
            }
        }
    }
}
