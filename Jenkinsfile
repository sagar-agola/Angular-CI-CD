pipeline {
    agent any
    stages {
        stage('move') {
          sh 'cd dist/angular-ci-cd/browser'
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
