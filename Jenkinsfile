node {
        stage('Checkout SCM'){
                git branch: 'master', url: 'https://github.com/raghavbuzz/jenkinpipedemo.git'
        }
        stage('Install Node Modules'){
                sh "npm install"
        }
        stage('Build'){
                sh "npm run build"        
        }        
        stage('Deploy'){
                sh "cp -avr /var/lib/jenkins/workspace/jenkinpipedemo/dist/demoapp/. /codies/angular"
        }
        stage('Post-Deploy'){                
                /* clean up workspace */
                deleteDir()
                /* clean up tmp directory */
                dir("${workspace}@tmp") {
                        deleteDir()
                }
                /* clean up script directory */
                dir("${workspace}@script") {
                        deleteDir()
                }                        
        }
}