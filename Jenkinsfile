pipeline {

    agent any

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
        }
        stage('Deploy to Apache2') {
            steps {
                sh 'rsync -avzP dist/keyshell/* /var/www/html/'
            }
        }
    }
}
