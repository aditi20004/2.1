pipeline {
    agent any
    
    environment {
        APP_NAME = 'your-app'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/aditi20004/2.1.git', branch: 'main'
            }
        }
        
        stage('Build') {
            steps {
                // Replace 'sh' with 'bat' for Windows
                bat 'mvn clean install'
            }
        }
        
        stage('Test') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
        
        stage('Code Quality Analysis') {
            steps {
                // For SonarQube, or other tools if installed on Windows
                bat 'mvn sonar:sonar'
            }
        }
        
        stage('Deploy') {
            steps {
                // Adjust this for Windows. If using Docker on Windows, use the correct Docker command
                bat 'docker-compose up -d'
            }
        }
        
        stage('Release') {
            steps {
                echo "Promoting application to production"
            }
        }
    }
    
    post {
        always {
            mail to: 'shrivastavaditi14@gmail.com',
                subject: "Pipeline ${currentBuild.fullDisplayName} completed",
                body: "Build ${currentBuild.result} \n Check the console output: ${env.BUILD_URL}"
        }
    }
}
