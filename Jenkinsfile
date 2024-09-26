pipeline {
    agent any

    environment {
        SHELL = "/bin/bash"
    }

    stages {
        stage('Build') {
            steps {
                sh '''
                echo "Building the project..."
                cargo build --release
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                echo "Running tests..."
                cargo test
                '''
            }
        }

        stage('Lint') {
            steps {
                sh '''
                echo "Linting the code..."
                cargo clippy -- -D warnings
                '''
            }
        }

        // You can add more stages here as needed.
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
