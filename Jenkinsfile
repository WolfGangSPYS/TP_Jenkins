pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = 'dockerhub-credentials' // ID des credentials Jenkins
        DOCKER_IMAGE_NAME = 'moncompte/myapp' // Nom de l'image sur Docker Hub
        DOCKER_TAG = 'latest' // Tag Docker
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Construire l’application...'
                    // Ajoutez les commandes nécessaires pour construire votre application ici
                }
            }
        }

        stage('Containérisation') {
            steps {
                script {
                    echo 'Création de l’image Docker...'
                    sh 'docker build -t $DOCKER_IMAGE_NAME:$DOCKER_TAG .'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    echo 'Connexion à Docker Hub...'
                    docker.withRegistry('https://registry.hub.docker.com', DOCKER_HUB_CREDENTIALS) {
                        sh 'docker push $DOCKER_IMAGE_NAME:$DOCKER_TAG'
                    }
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    echo 'Lancer le conteneur...'
                    sh 'docker run -d --name myapp-container -p 8080:8080 $DOCKER_IMAGE_NAME:$DOCKER_TAG'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline terminée.'
        }
    }
}
