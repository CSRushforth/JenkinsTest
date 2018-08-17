pipeline {
    agent any
    stages {
	stage('plan') {
		steps {
			withCredentials([azureServicePrincipal('a62cdfa8-c458-4cb0-b5b0-217e21c6aea3')]) {
				sh "/opt/terraform/terraform init"
				sh "set +e; /opt/terraform/terraform plan -out=plan.out -detailed-exitcode; echo \$? &gt; status"
			}
		}

	}
        stage('build') {
            steps {
                sh "terraform --version"
            }
        }
    }
}
