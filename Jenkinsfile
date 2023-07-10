pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Checkout source code from version control
                checkout scm

                // Install dependencies
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                // Run unit tests
                sh 'python -m unittest discover -s tests'
            }
        }

        stage('Package') {
            steps {
                // Create a Docker image
                sh 'docker build -t myecommerceapp .'
            }
        }

        stage('Deploy') {
            steps {
                // Provision infrastructure with Terraform
                sh 'terraform init'
                sh 'terraform apply -auto-approve'

                // Deploy the Docker image
                sh 'docker run -d -p 80:5000 myecommerceapp'
            }
        }
    }

    post {
        success {
            // Send a success notification
            sh 'echo "E-commerce app deployment was successful!"'
        }

        failure {
            // Send a failure notification
            sh 'echo "E-commerce app deployment failed!"'
        }
    }
}
