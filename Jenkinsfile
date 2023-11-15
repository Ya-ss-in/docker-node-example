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
                    docker.build('test-image-jenkins')
                }
            }
        }
        stage('Analyser l\'image avec Trivy') {
            steps {
                script {
                    docker.image('aquasec/trivy:latest').run("-v /var/run/docker.sock:/var/run/docker.sock test-image-jenkins")
                }
            }
        }
    }

    post {
        always {
            script {
                discordSend(
                    description: "Le build a ${currentBuild.result}", 
                    result: currentBuild.result, 
                    title: env.JOB_NAME, 
                    webhookURL: "https://discord.com/api/webhooks/1174322036416446474/zZJwGweVsgJ-0DL-Ytjq3NQ5-6K9jmSs1Zb6_KIxWfm7xkOiGVRCEok2yKRzfceTabIW"
                )
            }
        }
    }

    stages {
        stage('Déployer') {
            when {
                expression { currentBuild.resultIsBetterOrEqualTo('SUCCESS') }
            }
            steps {
                script {
                    docker.run('test-image-jenkins', '--name test-auto-jenkins -p 8000:8000 -d')
                }
            }
        }
    }
}    
