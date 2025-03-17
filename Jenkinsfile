pipeline {
    agent any

    environment {
        DB_DATABASE = 'fake'
        DB_USERNAME = 'root'
        DB_PASSWORD = 'Majestic@123'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/SwatiRauthan02/jenkins.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'composer install --no-dev --prefer-dist'
            }
        }

        stage('Run Migrations') {
            steps {
                sh 'php artisan migrate --force'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'php artisan test'
            }
        }

        stage('Deploy Application') {
            steps {
                sh 'rsync -avz --exclude "vendor" . user@localhost:/var/www/jenkins'
            }
        }

        stage('Clear Cache') {
            steps {
                sh 'php artisan cache:clear'
                sh 'php artisan config:clear'
            }
        }
    }
}
