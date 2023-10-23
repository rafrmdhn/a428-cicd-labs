pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Lint') {
            steps {
                sh 'npm run lint' 
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'  
            }
        }
        stage('Deploy') {
            steps {
                
            }
        }
    }
    post {
        success {
            echo 'Proyek berhasil dibangun dan diuji.'
        }
        unstable {
            echo 'Proyek tidak stabil.'
        }
        failure {
            echo 'Proyek gagal dibangun atau diuji.'
        }
    }
}
