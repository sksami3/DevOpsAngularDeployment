pipeline {
    agent any

    environment {
        ANGULAR_IMAGE = 'my-angular-app'
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:20' // Use a specific LTS version of Node.js
                    args '-u root' // Optional: Run Docker container as root
                }
            }
            steps {
                script {
                    // Set the working directory to your Angular project directory
                    //dir('path/to/your/angular/app') {
                        sh 'sudo systemctl start docker'
                        // Install project dependencies
                        sh 'docker build -t my-angular-app .'

                        // Build Angular app
                        sh 'docker run -d -p 8080:80 my-angular-app'
                    //}
                }
            }
        }
        stage('Test') {
            agent any
            steps {
                script {
                    // Add testing steps if you have any
                    echo 'Testing Angular app'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {

                    	sh 'docker run -d -p 8080:80 my-angular-app'

                    }
                
            }
        }
    }
    post {
        always {
            // Log out of Docker registry
            sh 'docker logout'
        }
    }
}
