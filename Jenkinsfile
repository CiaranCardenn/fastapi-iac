pipeline {
    agent any

    parameters {
        string(name: 'IMAGE_TAG', defaultValue: 'v1.0.10', description: 'Docker image version')
    }

    environment {
        ANSIBLE = "/opt/homebrew/bin/ansible-playbook"
        EC2_IP = "13.217.224.229"
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
                sh """
                echo "Checking app at http://${EC2_IP}"
                curl --max-time 20 http://${EC2_IP}
                """
            }
        }
    }
}
