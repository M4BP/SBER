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


		stage('Deploy to K8s')
		{
			steps{
				sshagent(['k8s-jenkins'])
				{
					sh 'scp -r -o StrictHostKeyChecking=no deployment.yaml ubuntu@146.185.210.123:/path'
					
					script{
						try{
							sh 'ssh ubuntu@146.185.210.123 kubectl apply -f /path/deployment.yaml --kubeconfig=/path/kube.yaml'

							}catch(error)
							{

							}
					}
				}
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
