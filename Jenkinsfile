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

        stage('Run Application') {
            steps {
                // Kill any running instance of the application
                bat 'taskkill /F /IM java.exe || echo "No running application to stop."'
                // Start the application
                bat 'java -jar target\\your-app.jar'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
