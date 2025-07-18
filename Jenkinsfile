pipeline {
    agent any

    tools {
        maven 'Maven 3.8.8'
        nodejs 'NodeJS'
        jdk 'Temurin JDK 17'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/qanitasyaf/login-system-springboot-react'
            }
        }

        stage('Build Frontend (React)') {
            steps {
                dir('login-system/login-system-frontend') {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Build Backend (Spring Boot)') {
            steps {
                dir('login-system/login') {
                    sh 'java -version'
                    sh 'mvn clean package -DskipTests' 
                }
            }
        }

        stage('Unit Test & Coverage') {
            steps {
                dir('login-system/login') {
                    sh 'mvn test' 
                }
            }
            post {
                always {
                    junit 'login-system/login/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Static Code Analysis (SAST) via Sonar') {
            steps {
                dir('login-system/login') {
                    sh """
                    mvn clean verify sonar:sonar \\
                    -Dsonar.projectKey=mentoring-task \\
                    -Dsonar.projectName='mentoring-task' \\
                    -Dsonar.host.url=http://sonarqube:9000 \\
                    -Dsonar.token=sqp_43e91e31ca27094009f34b720c1319588b1d6e68
                    """
                }
            }
        }

    } 

    post {
        always {
            cleanWs() 
        }
        success {
            echo 'Pipeline finished successfully! 🚀'
        }
        failure {
            echo 'Pipeline failed! 💥'
        }
    }
}
