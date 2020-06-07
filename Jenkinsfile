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
                bat 'rmdir -rf dist/'
                bat 'rmdir -rf dist.zip'
                bat 'npm install'
                bat 'NODE_OPTIONS="--max-old-space-size=8192" npm run build'
                echo 'building app'
            }
        }
        stage('Test') {
             steps {
                bat 'npm test'
                echo 'testing app'
             }
        }
        stage('Archive Artifacts') {
              steps {
        		bat 'zip -r dist.zip dist/'
        		step([$class: 'ArtifactArchiver', artifacts: 'dist.zip', fingerprint: true])
        		echo 'getting artifacts'
              }
        }
        stage('Deploy') {
               steps {
        	     //sh 'firebase deploy --debug'
        	     echo 'Deploying app'
               }
         }
    }
}
