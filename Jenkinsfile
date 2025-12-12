pipeline {
    agent any
    environment {
        TF_VAR_gcp_project = "<your GCP project ID here>" // REPLACE WITH YOUR PROJECT ID FROM QWIKLABS
    }
    stages {
        stage("Configure Cluster") {
            steps {
                script {
                    dir('terraform') {
                        withCredentials([file(credentialsId: 'gcp_credentials', variable:'GCP_CREDENTIALS')]) {
                            terraform init
                            terrascan scan -i terraform -t gcp
                            terraform apply -auto-approve
                        }
                    }
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}