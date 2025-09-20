def remote = [:]
remote.name = 'Ubuntu Server'
remote.host = '172.22.0.12'
remote.allowAnyHosts = true

pipeline {
    agent any

    environment {
        SERVER_CREDS = credentials('ubuntu-server')
    }
    stages {
        stage('Build') {
            steps {
                echo 'Starting build...'
                // sh 'apt-get update && apt-get install git rsync -y'
                sh """
                    rm -rf \$(pwd)/COSC2767-RMIT-Store
                    git clone "https://github.com/TomHuynhSG/COSC2767-RMIT-Store.git"
                """
            }
        }

        stage('Establish SSH Connection'){
            steps {
                echo 'Establishing SSH connection...'
                script {
                    remote.user = env.SERVER_CREDS_USR
                    remote.password = env.SERVER_CREDS_PSW
                    sshCommand (remote: remote,
                                command: "apt update && apt install git rsync -y"
                                )

                    sh """
                        rsync -avz -e "sshpass -p '${env.SERVER_CREDS_PSW}' ssh -o StrictHostKeyChecking=no" /var/jenkins_home/workspace/testing/COSC2767-RMIT-Store ${env.SERVER_CREDS_USR}@${remote.host}:/home/ubuntu/
                    """
                }
            
            }
        }
    }
}