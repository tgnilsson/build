pipeline {
	agent none
	stages {
		stage('Beginning') { agent any
			steps {
				echo 'Hellow world'
			}
		}

		stage('Who Am I?') {agent any
			steps {
				sh 'host -t TST pgp.michaelholley.us | awk -F\'"\' \'{print $2}\''
			}
		}
	}
}