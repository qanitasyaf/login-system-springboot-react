pipeline {
    agent any

    tools {
        // 'Maven' must match the 'Name' you gave in Global Tool Configuration for Maven
        maven 'Maven 3.8.8' 
        // 'NodeJS' must match the 'Name' you gave in Global Tool Configuration for NodeJS
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
                    // npm will be available in the PATH due to the 'nodejs' tool configuration
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Build Backend (Spring Boot)') {
            steps {
                dir('login-system/login') {
                    // mvn will be available in the PATH due to the 'maven' tool configuration
                    sh 'java -version'
                    sh 'mvn clean package -DskipTests' 
                }
            }
        }
        
        // ... rest of your stages
    }
}