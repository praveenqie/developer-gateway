pipeline {
    agent any

    environment {
        // Set environment variables if needed
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk' // Update to your system's Java version
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
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Run unit tests
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                // Package the application (e.g., JAR or WAR)
                sh 'mvn package'
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
