pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/Mohammeddalkha/CI-CD-Project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t portfolio .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker rm -f $(docker ps -q --filter ancestor=portfolio) || true'
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 80:80 portfolio'
            }
        }
    }
}
