pipeline {
    agent any
    stages {
	stage('plan') {
		steps {
			sh "/opt/terraform/terraform init"
			sh "set +e; /opt/terraform/terraform plan -out=plan.out -detailed-exitcode; echo \$? &gt; status"
		}

	}
        stage('build') {
            steps {
                sh "terraform --version"
            }
        }
    }
}
