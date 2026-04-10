pipeline {
    agent any

    parameters {
        string(name: 'IMAGE_TAG', defaultValue: 'v1.0.10', description: 'Docker image version')
    }

    environment {
        ANSIBLE = "/opt/homebrew/bin/ansible-playbook"
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
                ${ANSIBLE} -i inventory playbooks/deploy.yml \
                --extra-vars "image_tag=${params.IMAGE_TAG}"
                """
            }
        }

        stage('Health Check') {
            steps {
                sh "curl http://100.53.180.209"
            }
        }
    }
}
