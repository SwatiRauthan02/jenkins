pipeline {
    agent any

    environment {
        PHP_VERSION = "8.2"
        DB_DATABASE = "fake"
        DB_USERNAME = "root"
        DB_PASSWORD = "Majestic@123"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: ' https://github.com/SwatiRauthan02/jenkins.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'composer install --no-interaction --prefer-dist --optimize-autoloader'
            }
        }

        stage('Setup Environment') {
            steps {
                sh 'cp .env.example .env'
                sh 'php artisan key:generate'
            }
        }
    }

    post {
        success {
            echo "Deployment successful!"
        }
        failure {
            echo "Build failed!"
        }
    }
}
