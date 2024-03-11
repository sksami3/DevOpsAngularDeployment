pipeline {
    agent any

    environment {
        ANGULAR_IMAGE = 'my-angular-app'
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:14' // Use a specific LTS version of Node.js
                    args '-u root' // Optional: Run Docker container as root
                }
            }
            steps {
                script {
                    // Set the working directory to your Angular project directory
                    dir('path/to/your/angular/app') {
                        // Install Angular CLI
                        sh 'npm install -g @angular/cli'
                        
                        // Install project dependencies
                        sh 'npm install'

                        // Build Angular app
                        sh 'ng build --prod'
                    }
                }
            }
        }
        // Add other stages as needed (e.g., Test, Deploy)
    }
    post {
        always {
            // Log out of Docker registry
            sh 'docker logout'
        }
    }
}
