pipeline {
    agent any
    
    environment {
        DEPLOY_SERVER = '13.60.210.45'
        DEPLOY_USER = 'admin'
        DEPLOY_DIR = '/path/to/deployment/directory'
    }
    
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Akashp-devops/Jenkins-Calculator.git'  // Your GitHub repo URL
            }
        }
        
        stage('Build Application') {
            steps {
                script {
                    // Example of building a Java application with Maven
                    sh 'mvn clean install'
                }
            }
        }
        
        stage('Deploy Application') {
            steps {
                script {
                    // SSH into the server and deploy the app
                    sshagent(credentials: ['ssh-credentials-id']) {
                        sh """
                            ssh ${DEPLOY_USER}@${DEPLOY_SERVER} <<EOF
                                cd ${DEPLOY_DIR}
                                git pull origin main
                                # Replace this with the actual deployment command, e.g.:
                                # ./deploy.sh
                            EOF
                        """
                    }
                }
            }
        }
        
        stage('Clean Up') {
            steps {
                cleanWs()  // Cleans up workspace after the build and deploy
            }
        }
    }
    
    post {
        success {
            echo 'Deployment Successful!'
        }
        failure {
            echo 'Deployment Failed!'
        }
    }
}
