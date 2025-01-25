pipeline {
  agent {
    node {
      label 'build-in'
    }

  }
  stages {
    stage('Poll') {
      steps {
        sh 'scm checkout'
      }
    }

    stage('Build & Unit test') {
      steps {
        sh 'sh \'mvn clean verify -DskipITs=true\';'
        sh 'junit \'**/target/surefire-reports/TEST-*.xml\''
        sh 'archive \'target/*.jar\''
      }
    }

    stage('Static Code Analysis') {
      steps {
        sh 'sh \'mvn clean verify sonar:sonar -Dsonar.projectName=example-project -Dsonar.projectKey=example-project -Dsonar.projectVersion=$BUILD_NUMBER\';'
      }
    }

    stage('Integration Test') {
      steps {
        sh 'sh \'mvn clean verify -Dsurefire.skip=true\';'
        sh 'junit \'**/target/failsafe-reports/TEST-*.xml\''
        sh 'archive \'target/*.jar\''
      }
    }

    stage('Container Deploy') {
      steps {
        sh 'sh'
      }
    }

  }
}