pipeline {
    agent any

    environment {
        DEPLOY_SERVER = '51.20.116.95'           // Your server IP
        DEPLOY_USER = 'admin'                    // Server user
        DEPLOY_DIR = '/path/to/deployment/directory'  // Path where code is located on server
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Akashp-devops/Jenkins-Calculator.git'  
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Install Node.js packages
                    sh 'npm install'
                }
            }
        }

        stage('Deploy Application') {
            steps {
                script {
                    // SSH into server and pull latest code
                    sshagent(credentials: ['ssh-credentials-id']) {  
                        sh """
                            ssh -o StrictHostKeyChecking=no ${DEPLOY_USER}@${DEPLOY_SERVER} <<EOF
                                cd ${DEPLOY_DIR}
                                git pull origin main
                                npm install
                            EOF
                        """
                    }
                }
            }
        }

