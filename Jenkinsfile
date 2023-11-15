pipeline {
    agent any

    stages {
        stage('Cloner le dépôt') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[url: 'https://github.com/votre-utilisateur/votre-depot.git']]])
            }
        }

        stage('Construire l\'image Docker') {
            steps {
                script {
                    docker.build('test_jenkins')
                }
            }
        }

        stage('Tests unitaires') {
            steps {
                // Ajoutez les commandes pour exécuter les tests unitaires (si nécessaire)
            }
        }
    }

    post {
        success {
            discordSend(message: 'Le build a réussi !', color: '00FF00')
        }
        failure {
            discordSend(message: 'Le build a échoué.', color: 'FF0000')
        }
    }
}
