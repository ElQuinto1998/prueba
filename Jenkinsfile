pipeline {
    agent {
        any {
            image 'node:8-alpine'
            args '-p 3000:3000'
        }
    }
    environment {
        CI = 'true'
        FIREBASE_TOKEN = credentials('firebase-token')
    }
    stages {
        stage('Install dependencies') {
            steps {
                bat 'npm install'
                echo 'Installing dependencies'
            }
        }
        stage('Unit tests') {
             steps {
                bat 'npm test'
                echo 'Running unit tests'
             }
        }
        stage('Build') {
              steps {
                bat 'npm run build'
                echo 'Building app'
              }
        }
        stage('Deploy') {
               steps {
                 bat 'npm install -g firebase-tools'
        	     bat  'firebase deploy --debug'
        	     echo 'Deploying app'
               }
         }
    }
}
