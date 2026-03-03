pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Compile') {
      steps {
        sh './mvnw clean compile || mvn clean compile'
      }
    }

    stage('SONARQUBE') {
      environment {
        SONAR_HOST_URL = 'http://192.168.33.10:9000'
        SONAR_AUTH_TOKEN = credentials('sonarqube')
      }
      steps {
        // Analyse SonarQube
        sh './mvnw sonar:sonar -Dsonar.projectKey=devops_git -Dsonar.host.url=$SONAR_HOST_URL -Dsonar.token=$SONAR_AUTH_TOKEN || mvn sonar:sonar -Dsonar.projectKey=devops_git -Dsonar.host.url=$SONAR_HOST_URL -Dsonar.token=$SONAR_AUTH_TOKEN'
      }
    }
  }
}
