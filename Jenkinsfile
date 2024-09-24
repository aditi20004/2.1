pipeline {
    agent any
    
    environment {
        APP_NAME = 'your-app'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/aditi20004/2.1.git', branch: 'master'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
        
        stage('Code Quality Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'docker-compose up -d'
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
            mail to: 'youremail@example.com',
                subject: "Pipeline ${currentBuild.fullDisplayName} completed",
                body: "Build ${currentBuild.result} \n Check the console output: ${env.BUILD_URL}"
        }
    }
}
