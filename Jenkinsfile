node {
        stage('Checkout SCM'){
                git branch: 'master', url: 'https://github.com/raghavbuzz/jenkinpipedemo.git'
        }

        stage('Install node modules'){
                sh "npm install"
        }
        stage('Build'){
                sh "npm run build-prod"
        }
        stage('Deploy'){
                sh "cp -avr /var/lib/jenkins/workspace/jenkinpipedemo/dist/demoapp/. /codies/angular"
        }
        stage('Post Deploy'){
            cleanWs()
        }
    }
}
