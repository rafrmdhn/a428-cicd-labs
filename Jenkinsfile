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
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Manual Approval') {
            steps {
                input(
                    id: 'manual',
                    message: 'Lanjutkan ke tahap Deploy?',
                    submitter: 'admin', 
                    parameters: [booleanParam(name: 'proceed', defaultValue: true, description: 'Klik "Proceed" untuk melanjutkan')]
                )
            }
        }
        stage('Deploy') {
            when {
                expression { currentBuild.rawBuild.getAction(ParametersAction)?.parameters['proceed'].value }
            }
            steps {
                sh './jenkins/scripts/deliver.sh'
                sh 'sleep 1m'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
    post {
        success {
            echo 'Proyek berhasil dibangun, diuji, dan di-deploy.'
        }
        unstable {
            echo 'Proyek tidak stabil.'
        }
        failure {
            echo 'Proyek gagal dibangun, diuji, atau di-deploy.'
        }
    }
}
