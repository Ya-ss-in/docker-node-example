pipeline {
    agent any

    stages {
        stage('Cloner le dépôt') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/Ya-ss-in/docker-node-example.git']]])
            }
        }

        stage('Construire l\'image Docker') {
            steps {
                script {
                    docker.build('test-yassin-jenkins')
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
