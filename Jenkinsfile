node('built-in') {
  
  stage('Poll') {
    checkout scm
  }

  stage('Build & Unit test') {
    sh 'mvn clean verify -DskipITs=true';
    junit '**/target/surefire-reports/TEST-*.xml'
    archive 'target/*.jar'
  }

  stage('Static Code Analysis') {
    sh 'mvn clean verify sonar:sonar -Dsonar.projectName=example-project -Dsonar.projectKey=example-project -Dsonar.projectVersion=$BUILD_NUMBER';
  }

  // stage ('Publish') {
    
  // }
}
