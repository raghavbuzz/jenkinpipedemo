pipeline {
  agent none
  stages {
    stage('Fetch Dependencies') {
      agent {
        docker 'node:10.14.0-alpine'
      }
      steps {
        sh 'npm install -g @angular/cli'
        sh 'npm install'
        stash includes: 'node_modules/', name: 'node_modules'
      }
      post {
        success {
          slackSend (color: "#00FF00", message:"Success: Fetch Dependencies ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)")
        }
        failure {
          slackSend (color: "#FF0000", message:"Failed: Fetch Dependencies ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)")
        }
      }
    }	
	stage('Compile Browser') {
       agent {
        docker 'node:10.14.0-alpine'
      }
      steps {
        unstash 'node_modules'
        sh 'npm run build --prod'
      } 
      post {
        success {
          slackSend (color: "#00FF00", message:"Success: Browser compile ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)")
        }
        failure {
          slackSend (color: "#FF0000", message:"Failed: Browser compile ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)")
        }
      }
    }
	stage('Compile SSR') {
      agent {
        docker 'node:10.14.0-alpine'
      }
      steps {
        unstash 'node_modules'
        sh 'npm run build:server'
        sh 'npm run webpack:server'
      } 
      post {
        success {
          slackSend (color: "#00FF00", message:"Success: SSR compile ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)")
        }
        failure {
          slackSend (color: "#FF0000", message:"Failed: SSR compile ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)")
        }
      }
    }
	stage('Deploy Prod') {
      agent any
      environment {
          TAG = sh (script: "git log -n 1 --pretty=format:'%h'", returnStdout: true)
      }
      steps {
        echo "${env.TAG}"
        sh "sudo docker build -t educatex_prod:${env.TAG} -f app.dockerfile ."                
        sh 'sudo -E docker stack deploy -c docker-compose.prod.yml educatex'        
        sh 'sudo docker-compose -f docker-compose.prod.yml -p PROD up -d'**/
      }
      post {
        success {
          slackSend (color: "#00FF00", message:"Success: Deploy Prod ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)")
        }
        failure {
          slackSend (color: "#FF0000", message:"Failed: Deploy Prod ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)")
        }
      }
    }
    stage('Clean') {
      agent any
      steps {        
        sh 'sudo docker system prune -f'
      }
    }
  }
}
