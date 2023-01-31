pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub-sber-viktor')
	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t imagine1337/sberapp:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push imagine1337/sberapp:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
