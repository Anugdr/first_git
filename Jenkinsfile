
pipeline {
    agent any

 //options {
 //   disableConcurrentBuilds()
 //    timestamps()
//} 

    parameters {
         choice choices: ['https://github.com/Anugdr/first_git.git', 'https://github.com/Anugdr/jenkins_pipeline.git'], description: 'choose URl to checkout', name: 'GIT_URL'
        choice(name:'SERVER',choices: ['test','staging','prod'])
        string(name: 'CHECKOUT_BRANCH',defaultValue: 'main')
      }

    
    environment {
      APP_NAME ='Frontend'
      TARGET_ENV ='Backend'
      CHECKOUT_BRANCH='main'
  }
    
    stages {
        stage('parllel'){
            
            parallel {
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
           
            }
        }

                 stage('prepare') {
              steps {
               cleanWs()//clean workspace
                

            }
        }
        
        
        stage('env') {
        steps {
          sh "echo  ${env.APP_NAME}"
                 
                sh '''
                echo $APP_NAME
                '''
                }
                }
        
        stage('build') {
            agent { label 'slave1' }
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


        stage('A') {
            steps {
                echo 'This is stage A'
            }
        }

        stage('B') {
            steps {
                echo 'This is stage B'
                catchError(stageResult: 'FAILURE', buildResult: 'SUCCESS')
                {
                    sh 'exit 1'
                }
            }
        }

        stage('C') {
            steps {
                echo 'continue to next stage'
            }
        }
    }
}
