pipeline {
    agent any

    environment {
        JAVA_HOME = 'C:\\Program Files\\Java\\jdk-17' // Update to your system's Java path
        PATH = "${env.PATH};${JAVA_HOME}\\bin"
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the Git repository
                git branch: 'main', url: 'https://github.com/praveenqie/developer-gateway.git'
            }
        }

        stage('Build') {
            steps {
                // Clean and build the project using Maven
                bat 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Run unit tests
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                // Package the application (e.g., JAR or WAR)
                bat 'mvn package'
            }
        }

        stage('Docker Build') {
            steps {
                // Build a Docker image
                bat 'docker build -t developer-gateway:latest .'
            }
        }

        stage('Docker Run') {
            steps {
                // Stop any running container
                bat 'docker stop developer-gateway || echo "No container to stop."'
                bat 'docker rm developer-gateway || echo "No container to remove."'

                // Run the Docker container
                bat 'docker run -d -p 8080:8080 --name developer-gateway developer-gateway:latest'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
