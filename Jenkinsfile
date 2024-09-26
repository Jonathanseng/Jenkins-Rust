pipeline {
    agent any

    environment {
        // Correctly append to the PATH variable using PATH+EXTRA
        PATH+EXTRA = "/Users/hokborithy/.nvm/versions/node/v16.20.2/bin"
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
