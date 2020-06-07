pipeline {
    agent {
        any {
            image 'node:8-alpine'
            args '-p 3000:3000'
        }
    }
    environment {
        CI = 'true'
        FIREBASE_DEPLOY_TOKEN = credentials('firebase-deploy-token')
    }
    stages {
        stage('Build') {
            steps {
                bat 'npm install'
            }
        }
        stage('Test') {
             steps {
                bat 'npm test'
             }
        }
        stage('Archive Artifacts') {
              steps {
                bat 'npm run build'
        		//bat 'zip -r build.zip build/'
        		//step([$class: 'ArtifactArchiver', artifacts: 'build.zip', fingerprint: true])
              }
        }
        stage('Deploy') {
               steps {
                 bat 'npm install -g firebase-tools'
        	     bat firebase deploy -P --debug --token "$FIREBASE_DEPLOY_TOKEN"
        	     echo 'Deploying app'
               }
         }
    }
}
