pipeline {
    agent any
    tools {
        nodejs '16.17.0'
    }
  
    options {
        retry(2)
        timestamps()
    }
  
    stages {
        stage('SCM') {
            steps {
                git branch: 'master', url: 'https://github.com/ajilraju/keyshell.git'
            }
        }
        stage('Install Deps') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                sh 'ng build'
            }
            post {
                success {
                    fingerprint 'dist/keyshell'
                }
            }
        }
        stage('Deploy to Apache2') {
            steps {
                sh 'rsync -avzP dist/keyshell/* /var/www/html/'
            }
        }
        stage('Archive Artifacts') {
            steps {
                sh '''
                  zip -r archive.zip dist/keyshell/*
                '''
                archiveArtifacts artifacts: 'archive.zip', fingerprint: true, onlyIfSuccessful: true
            }
        }
    }
}
