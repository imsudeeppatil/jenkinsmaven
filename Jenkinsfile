pipeline {
    agent any

    tools {
        maven 'Maven'  // Ensure this matches the Maven installation name in Jenkins
    }

    stages {
        // Stage to checkout code from GitHub
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/imsudeeppatil/jenkinsmaven.git'  // Replace with your GitHub repo URL if different
            }
        }

        // Stage to build the project using Maven
        stage('Build') {
            steps {
                sh 'mvn clean package'  // Build the project and create the JAR
            }
        }

        // Stage to run tests using Maven
        stage('Test') {
            steps {
                sh 'mvn test'  // Run tests using Maven
            }
        }

        // Stage to run the application after successful build and test
        stage('Run Application') {
            steps {
                script {
                    // Ensure the JAR is built with the correct Main-Class attribute
                    def jarFile = 'target/mavenjenkins-1.0-SNAPSHOT.jar'
                    if (fileExists(jarFile)) {
                        sh "java -jar ${jarFile}"  // Running the JAR file after building it
                    } else {
                        error "JAR file not found!"
                    }
                }
            }
        }
    }

    post {
        // Post actions after the build
        success {
            echo '✅ Build and deployment successful!'
        }
        failure {
            echo '❌ Build failed!'
        }
    }
}

