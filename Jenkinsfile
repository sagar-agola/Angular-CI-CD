pipeline {
    agent {
      docker {
        image 'node:22.13-alpine'
        label 'red-host'
      }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'ng build'
                sh 'cd dist/angular-ci-cd'
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
