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
            }
        }

        stage('Establish SSH Connection'){
            steps {
                echo 'Establishing SSH connection...'
                script {
                    remote.user = env.SERVER_CREDS_USR
                    remote.password = env.SERVER_CREDS_PSW
                    sshCommand (remote: remote,
                                command: """
                                    apt update &&
                                    apt install git npm -y &&
                                    rm /home/ubuntu/* -rf &&
                                    cd /home/ubuntu &&
                                    git clone "https://github.com/TomHuynhSG/COSC2767-RMIT-Store.git" &&
                                    echo 'Setup complete'
                                """.stripIndent().trim()
                                )
                }
            
            }
        }
    }
}