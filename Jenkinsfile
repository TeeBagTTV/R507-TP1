pipeline {
    agent any  // Cela indique que le pipeline peut être exécuté sur n'importe quel agent Jenkins
    stages {
        // Étape 1 : Construire l'image Docker
        stage('Build Docker Image') {
            steps {
                script {
                    // Construire l'image Docker
                    sh 'docker build -t devops-app .'
                }
            }
        }
        
        // Étape 2 : Push vers Docker Hub
        stage('Push to Docker Hub') {
            steps {
                script {
                    // Authentification Docker Hub avec les identifiants Jenkins
                    withCredentials([usernamePassword(
                        credentialsId: 'docker-hub-creds',  // Remplacez cela par votre credentialsId dans Jenkins
                        usernameVariable: 'marinlafitte',
                        passwordVariable: 'Marino0645'
                    )]) {
                        // Connexion à Docker Hub
                        sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                        
                        // Taguer l'image Docker avec votre nom d'utilisateur Docker Hub
                        sh 'docker tag devops-app $DOCKER_USERNAME/devops-app'
                        
                        // Pousser l'image vers Docker Hub
                        sh 'docker push $DOCKER_USERNAME/devops-app'
                    }
                }
            }
        }
    }
}
