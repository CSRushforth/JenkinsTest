pipeline {
    agent any
    stages {
	stage('init') {
			withCredentials([azureServicePrincipal('a62cdfa8-c458-4cb0-b5b0-217e21c6aea3')]) {
				ARM_SUBSCRIPTION_ID=env.AZURE_SUBSCRIPTION_ID
				ARM_CLIENT_ID=env.AZURE_CLIENT_ID
				ARM_CLIENT_SECRET=env.AZURE_CLIENT_SECRET
				ARM_TENANT_ID=env.AZURE_TENANT_ID
			}
	}
	stage('plan') {
		steps {
			sh "/opt/terraform/terraform init"
			sh """
				set +e
				export ARM_SUBSCRIPTION_ID=$ARM_SUBSCRIPTION_ID
				export ARM_CLIENT_ID=$ARM_CLIENT_ID
				export ARM_CLIENT_SECRET=$ARM_CLIENT_SECRET
				export ARM_TENANT_ID=$ARM_TENANT_ID
				export ARM_ENVIRONMENT=public
				env
				/opt/terraform/terraform plan -out=plan.out -detailed-exitcode
				echo \$? &gt
				status
			"""
		}

	}
        stage('build') {
            steps {
                sh "terraform --version"
            }
        }
    }
}
