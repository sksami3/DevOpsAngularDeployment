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
                    // Log in to Docker registry
                    withCredentials([usernamePassword(credentialsId: "${DOCKER_REGISTRY_CREDS}", passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                        sh "echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin docker.io"
                        
                        // Push Docker image
                        sh "docker push $ANGULAR_IMAGE"
                    }
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
