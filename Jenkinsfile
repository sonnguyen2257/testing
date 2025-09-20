def remote = [:]
remote.name = 'Ubuntu Server'
remote.host = '172.22.0.12'
remote.allowAnyHosts = true

pipeline {
    agent any

    enviroment {
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
                remote.user = env.SERVER_CREDS_USR
                remote.password = env.SERVER_CREDS_PSW

                sshCommand(remote: remote, command: 'echo "SSH connection establised on jenkins server" >> /home/ubuntu/output.txt')
            }
        }
    }
}