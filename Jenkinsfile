@Library(['jenkins-library','shared-library']) _

pipeline {
	agent none

							//3 things in the global: environment, post, 
	environment { 			//global environment variables, put the unique stuff here
		NODE_VER = '8.1.0'
	}

//	post {					
		// must go at the top so it will run this if it errors after, no access to the workspace
		//success slacksend here
		//failure
		//always
		//unstable
		//abort
//	}
//	tools { 
		//access to the global tools confuration
//}

//	options {				
	//global configurations like timeout, skipDefaultCheckout()
	//every step checks out code, unless you do the skip and manually chekcout
//	}



	stages {
		stage('Beginning') { agent any

			environment {	
							//stage environment variables
				DEPLOY_VERSION = 'stage'
			}
			steps {
				echo 'Hellow world'
				sh 'echo $NODE_VER'
				echo "${env.DEPLOY_VERSION}"
			}
		}

		stage('Who Am I?') { agent any
			environment {
				DEPLOY_VERSION = 'prod'
			}
			steps {
				echo "${env.DEPLOY_VERSION}" 
				sh 'host -t TXT pgp.michaelholley.us | awk -F\'"\' \'{print $2}\''
			}
		}

							// this part lets you come resond in the UI! for prod deploy! you can do response, multiple choice, boolean, text box, etc.

		stage('Deploy to stage?') { agent none
			when {
				anyOf{
					branch 'stage'
					environment name: 'NODE_VER', value: '8.1.0'
				}
			}
			steps {
				input 'Deploy to stage?'
			}
		}

		stage('Parallel') {
			failFast true	
							//if running parallel, fail them ALL immediately if any fails, don't finish the build
			parallel {
				stage('Build1') { agent any
					steps {
						echo "It's ME!"
						hello()
					}
				}

				stage('Build2') { agent any
					steps {
						echo "No it's me!"
					}
				}
			}
		}
	}
}