pipeline {
    agent any

    environment {
        // Set environment variables if needed
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

        stage('Deploy') {
            steps {
                // Deploy the application (optional, depending on your setup)
                echo 'Deploying the application...'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
