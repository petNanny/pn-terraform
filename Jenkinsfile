pipeline {
    agent any

    tools {
        terraform 'Terraform'
    }

    stages {
        stage('TF init & plan') {
            steps {
                sh 'export AWS_PROFILE=PNTerraform'
                sh 'terraform init'
                sh 'terraform validate'
                sh 'terraform plan -out tfplan'
                sh 'terraform show -no-color tfplan > tfplan.txt'
            }
        }
        stage('TF apply') {
            steps {
                sh 'terraform apply -input=false tfplan'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'tfplan.txt', onlyIfSuccessful: true
            cleanWs()
            sh 'ls -la'
        }
    }
}
