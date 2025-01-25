pipeline {
  agent build-in
  tools {
    maven('M3")
  }
  
  stage('Poll') {
    checkout scm
  }

  stages {
    stage('Build & Unit test') {
      sh 'mvn clean verify -DskipITs=true';
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
    }

    stage('Static Code Analysis') {
      sh 'mvn clean verify sonar:sonar -Dsonar.projectName=example-project -Dsonar.projectKey=example-project -Dsonar.projectVersion=$BUILD_NUMBER';
    }

    // stage ('Publish') {}
  }
}
