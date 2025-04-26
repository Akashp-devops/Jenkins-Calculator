pipeline {
    agent any

    environment {
        DEPLOY_SERVER = '51.20.116.95'           // Your server IP
        DEPLOY_USER = 'admin'                    // Server user
        DEPLOY_DIR = '/path/to/deployment/directory'  // Deployment path
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
                    sh 'npm install'
                }
            }
        }

        stage('Deploy Application') {
            steps {
                script {
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

        stage('Clean Up') {
            steps {
                cleanWs()
            }
        }
    }

    post {
        success {
            echo '🎉 Deployment Successful!'
        }
        failure {
            echo '❌ Deployment Failed!'
        }
    }
}
