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
        script {
            // Find any container using port 80
            def oldContainerId = sh(
                script: "docker ps -q --filter 'publish=80'",
                returnStdout: true
            ).trim()

            if (oldContainerId) {
                sh "docker rm -f ${oldContainerId}"
                echo "Old container on port 80 stopped: ${oldContainerId}"
            } else {
                echo "No container using port 80"
            }
        }
    }
}


        stage('Run New Container') {
            steps {
                sh 'docker run -d --rm -p 80:80 --name portfolio_container portfolio'

            }
        }

        stage('Cleanup Unused Images') {
            steps {
                sh 'docker image prune -f'
            }
        }
    }
}
