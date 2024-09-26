pipeline {
    agent any  // Use any available agent (Jenkins node)
    
    // Define environment variables (optional)
    environment {
        CARGO_HOME = "${WORKSPACE}/.cargo" // Define a custom cargo home directory (optional)
    }

    stages {
        // Stage 1: Check out the code from the repository
        stage('Checkout') {
            steps {
                checkout scm // This checks out the source code from the repository
            }
        }

        // Stage 2: Build the project using `cargo build`
        stage('Build') {
            steps {
                sh 'cargo build --release' // Build the project in release mode
            }
        }

        // Stage 3: Run unit tests using `cargo test`
        stage('Test') {
            steps {
                sh 'cargo test' // Run all tests
            }
        }

        // Stage 4: Lint the code using `cargo clippy`
        stage('Lint') {
            steps {
                sh 'cargo clippy -- -D warnings' // Lint the code and fail on warnings
            }
        }

        // Stage 5: Code Coverage (Optional)
        stage('Code Coverage') {
            steps {
                sh 'cargo tarpaulin --out Html' // Generate code coverage report
                publishHTML(target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'target/tarpaulin-report',
                    reportFiles: 'index.html',
                    reportName: 'Coverage Report'
                ])
            }
        }

        // Stage 6: Deploy the project (Optional)
        stage('Deploy') {
            when {
                branch 'main' // Only deploy when on the 'main' branch
            }
            steps {
                sh './deploy.sh' // Call your deployment script
            }
        }
    }

    // Post actions: Always run steps here regardless of success or failure
    post {
        always {
            archiveArtifacts artifacts: 'target/release/**', allowEmptyArchive: true // Archive build artifacts
            junit 'target/test-results/*.xml' // Store test results in JUnit format if available
        }
        success {
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Build or tests failed.'
        }
    }
}

