pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'ls'
                sh 'npm install'
                sh 'echo N | ng analytics off'
                sh 'ng build'
                sh 'ls'
                sh 'cd dist && ls'
                sh 'cd dist/angular-ci-cd && ls'
            }
        }
        stage('S3 Upload') {
            steps {
                withAWS(region: 'us-east-1', credentials: 'AWS S3 Full Access') {
                    sh 'ls -la'
                    sh 'aws s3 cp dist/angular-ci-cd/. s3://angular-ci-cd/ --recursive'
                }
            }
        }
    }
}
