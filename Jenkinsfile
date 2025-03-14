pipeline {
    agent any

    environment {
        APACHE_DIR = '/var/www/html'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Tochi-Nwachukwu/seeAfrika.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh 'echo test'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    sh 'npm run build'
                }
            }
        }

        stage('Deploy to Apache') {
            steps {
                script {
                    sh """
                    sudo rm -rf $APACHE_DIR/*
                    sudo cp -r dist/* $APACHE_DIR/
                    sudo chown -R www-data:www-data $APACHE_DIR
                    sudo chmod -R 755 $APACHE_DIR
                    sudo systemctl restart apache2
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment to Apache Server successful!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}