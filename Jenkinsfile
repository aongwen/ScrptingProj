pipeline{
	agent any
	parameters {
		string(name: 'VERSION', defaultValue: '', description: 'Version to deploy on prod')
		choice(name: 'VERSION', choices: ['1.1.0','1.2.0','1.3.0'], description: '')
		booleanParam(name: 'executeTests', defaultValue: true, description: '')
	}
	environment {
		NEW_VERSION = '1.3.0'
		SERVER_CREDENTIALS = credentials('server-credentials')
	}
	Stages{
	stage("build"){
		steps {
		echo "building the application"
		}
	}

	stage("test"){
		when{
			expression{
				BRANCH_NAME == 'dev' || BRANCH_NAME == 'master'
			}
		}
		steps {
		echo "testing the application"
		}
	}
	stage("deploy"){
		steps {
		echo "deploying the application"
		withCredentials([
		usernamePassword(credentials: 'server-credentials', usernameVariable: USER, passwordVariable: PWD)
		]){
			sh "some script ${USER} ${PWD}"
		}
		}
	}
   }
}
