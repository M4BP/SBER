pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub-sber-viktor')
	}

	stages {

		stage('Build') {

			steps {
				sh 'sudo docker build -t viktor/sberapp:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'sudo docker push viktor/sberapp:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
