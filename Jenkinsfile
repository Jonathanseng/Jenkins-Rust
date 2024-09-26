pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''
                /bin/bash -c "echo Building the project..."
                /bin/bash -c "cargo build --release"
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                /bin/bash -c "echo Running tests..."
                /bin/bash -c "cargo test"
                '''
            }
        }

        stage('Lint') {
            steps {
                sh '''
                /bin/bash -c "echo Linting the code..."
                /bin/bash -c "cargo clippy -- -D warnings"
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
