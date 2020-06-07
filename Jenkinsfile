pipeline {
    agent {
        any {
            image 'node:6-alpine'
            args '-p 3000:3000'
        }
    }
    environment {
            CI = 'true'
        }
    stages {
        stage('Build') {
            steps {
                bat 'whoami'
                bat 'npm install'
                bat 'npm run build'
                echo 'building app'
            }
        }
        stage('Test') {
             steps {
                bat 'npm test'
             }
        }
        stage('Archive Artifacts') {
              steps {
        		bat 'zip -r build.zip build/'
        		step([$class: 'ArtifactArchiver', artifacts: 'build.zip', fingerprint: true])
              }
        }
        stage('Deploy') {
               steps {
        	     bat 'firebase deploy --debug'
        	     echo 'Deploying app'
               }
         }
    }
}
