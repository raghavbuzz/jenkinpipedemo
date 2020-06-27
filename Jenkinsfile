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
                // sh "npm run build-prod"
        }
        post { 
          always { 
            cleanWs()
        }
    }
}
