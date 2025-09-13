
pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
               git credentialsId: 'apps_github', url: 'https://github.com/Anugdr/first_git.git',branch: 'main'


            }
        }
 stage('checkout2') {
            steps {
               

checkout scmGit(branches: [[name: '*/main']], userRemoteConfigs: [[credentialsId: 'apps_github', url: 'https://github.com/Anugdr/first_git.git']])
            }
        }
        stage('build') {
            steps {
                sh '''
                pwd
                ls -lrt
                '''
                
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
            }
        }
    }
}
