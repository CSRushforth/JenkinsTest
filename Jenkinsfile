pipeline {
    agent any
    stages {
	stage('plan') {
		steps {
			sh "ls -al"
			sh "set +e; /opt/bin/terraform plan -out=plan.out -detailed-exitcode; echo \$? &gt; status"
		}

	}
        stage('build') {
            steps {
                sh "terraform --version"
            }
        }
    }
}
