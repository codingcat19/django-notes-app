pipeline {
    agent { label "any" }

    stages {
        stage("Code Clone") {
            steps {
                clone("https://github.com/codingcat19/django-notes-app.git", "main")
                echo "Clone Completed"
            }
        }

        stage("Build") {
            steps {
                script {
                    sh "sh "docker build -t codingcat19/notes-app:latest .""
                    echo "Build complete"
                }
            }
        }

        stage("Dockerhub Login") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerHubCred'
                usernameVariable: 'DOCKERHUB_USERNAME',
                passwordVariable: 'DOCKERHUB_PASSWORD')]) {
                    sh 'docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
                }
            }
        }

        stage("Push to dockerhub") {
            steps {
                sh "docker push codingcat19/notes-app:latest"
            }
        }
    }
}