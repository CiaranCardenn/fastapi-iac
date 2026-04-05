pipeline {
    agent any

    parameters {
        string(name: 'IMAGE_TAG', defaultValue: 'v1.0.10', description: 'Docker image version')
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Deploy') {
            steps {
                sh """
                ansible-playbook -i inventory playbooks/deploy.yml \
                --extra-vars "image_tag=${params.IMAGE_TAG}"
                """
            }
        }

        stage('Health Check') {
            steps {
                sh "curl 54.160.200.28"
            }
        }
    }
}
