pipeline{

	agent {label 'devopsvm2'}

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git 'https://github.com/akank12/nodeapp_test.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t akank12/nodeapp_test:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push akank12/nodeapp_test:latest'
			}
		}
	}
               stage('Pull') {
                                sh 'docker pull akank12/nodeapp_test:latest'
                         }
               }
      }
               stage('Run') {
                                sh 'docker run -d --name nodecont -p 3001:3000 akank12/nodeapp_test:latest'
                        }
               }
    }
	post {
		always {
			sh 'docker logout'
		}
	}

}
