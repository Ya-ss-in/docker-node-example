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
                    docker.build('nom-image')
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
            script {
                discordSend(description: "Le build a réussi !", result: "SUCCESS", title: env.JOB_NAME, webhookURL: "https://discord.com/api/webhooks/1174322036416446474/zZJwGweVsgJ-0DL-Ytjq3NQ5-6K9jmSs1Zb6_KIxWfm7xkOiGVRCEok2yKRzfceTabIW")
            }
        }
        failure {
            script {
                discordSend(description: "Le build a échoué.", result: "FAILURE", title: env.JOB_NAME, webhookURL: "https://discord.com/api/webhooks/1174322036416446474/zZJwGweVsgJ-0DL-Ytjq3NQ5-6K9jmSs1Zb6_KIxWfm7xkOiGVRCEok2yKRzfceTabIW")
            }
        }
    }
}
