pipeline {
    agent any

    stages {
        stage("Code Clone") {
            steps {
                git branch: 'main', url: 'https://github.com/codingcat19/django-notes-app.git'
                echo "Clone Completed"
            }
        }

        stage("Build") {
            steps {
                script {
                    sh "docker build -t codingcat19/notes-app:latest ."
                    echo "Build complete"
                }
            }
        }

        stage("Dockerhub Login") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerHubCred',
                                                  usernameVariable: 'DOCKERHUB_USERNAME',
                                                  passwordVariable: 'DOCKERHUB_PASSWORD')]) {
                    sh 'docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
                }
            }
        }

        stage("Push to dockerhub") {
            steps {
                success {
                    sh "docker push codingcat19/notes-app:latest"
                }
            }
        }
    }
}