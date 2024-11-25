pipeline {
    agent any

    environment {
        JAVA_HOME = 'C:\\Program Files\\Java\\jdk-17'
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
                script {
                    // Identify any existing process running the application and terminate it
                    def pid = bat(returnStdout: true, script: 'netstat -ano | findstr :8080').trim()
                    if (pid) {
                        bat "taskkill /PID ${pid} /F"
                        echo 'Terminated existing application instance.'
                    } else {
                        echo 'No running instance found.'
                    }

                    // Start the application in the background
                    bat 'start cmd /c "java -jar target\\developer-gateway-*.jar > log.txt 2>&1"'
                    echo 'Application started successfully.'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
