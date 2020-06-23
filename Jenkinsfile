pipeline {
	agent { dockerfile true }
	stages {
		stage('One'){
			steps{
				echo 'Starting Build'
			}
		}		
		stage ('install modules'){
			steps{
				// sh 'npm install'
				echo 'install modules'
			}
		}
		stage ('build'){
			steps{
				// sh 'npm run build-prod'
				echo 'build'
			}
		}
		// stage ('pre-deploy'){
		// 	steps{
		// 		bat 'del /q "C:\\Raghav\\Codies\\Hosting\\jenkinpipelinedemo\\*"'
		// 	}
		// }		
		// stage ('deploy'){			
		// 	steps{
		// 		bat 'xcopy dist\\Angular8POC "C:\\Raghav\\Codies\\Hosting\\jenkinpipelinedemo" /O /X /E /H /K'
		// 	}
		// }
	}
	post {
        always {
            echo 'One way or another, I have finished'
            // deleteDir()
			dir("${workspace}@tmp") {
                deleteDir()
            }            
            dir("${workspace}@script") {
                deleteDir()
            }
        }
        success {
            echo 'I succeeeded! :)'
        }
        unstable {
            echo 'I am unstable :/'
        }
        failure {
            echo 'I failed :('
        }
        changed {
            echo 'Things were different before...'
        }
    }	
}