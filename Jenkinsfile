pipline {
    agent any
    parameters {
        string(name : 'Environment', description: 'production')
    }
    
    stages {
        stage("Pull from ECR") {
            steps {
                sh 'rm -rf maven-sample'
                sh 'aws ecr-public get-login-password --region us-east-1 | helm registry login --username AWS --password-stdin public.ecr.aws/k3b8b1b7'
                sh 'helm pull oci://public.ecr.aws/k3b8b1b7/maven-sample --version 1.${params.buildnumber}.1 --untar'
            }
        }
        stage("Deploy to Minikube") {
            steps {
                sh 'helm install maven-sample maven-sample'
            }
        }
    }
}