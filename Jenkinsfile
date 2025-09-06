pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/PadhmaGanesh/Rohan.git'
            }
        }

        stage('Deploy to Nginx Server') {
            steps {
                sshagent(['ec2-ssh-key']) {
                    sh '''
                    # Copy file to Nginx server
                    scp -o StrictHostKeyChecking=no index.html ec2-user@13.233.173.240:/usr/share/nginx/html/index.html
                    
                    # Restart Nginx
                    ssh ec2-user@13.233.173.240 "sudo systemctl restart nginx"
                    '''
                }
            }
        }
    }
}
