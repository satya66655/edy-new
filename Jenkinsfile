pipeline {
    agent any

    environment {
        EC2_HOST = 'ec2-user@13.233.145.58'
        SSH_KEY_ID = 'ec2-ssh-key' // Jenkins credential ID
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/satya66655/edy-new.git'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent (credentials: [env.SSH_KEY_ID]) {
                    sh 'scp -o StrictHostKeyChecking=no index.html $EC2_HOST:/var/www/html/index.html'
                }
            }
        }
    }

    post {
        success {
            echo "Deployment completed successfully."
        }
        failure {
            echo "Deployment failed."
        }
    }
}
