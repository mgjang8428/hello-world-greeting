node ('built-in') {

  def mvnHome

  stage('Preparation') {
    mvnHome = tool 'M3'
  }
    
  stage('Poll') {
    checkout scm
  }
  
  stage('Build & Unit test') {
    sh "'${mvnHome}/bin/mvn' clean verify -DskipITs=true";
    junit '**/target/surefire-reports/TEST-*.xml'
    archive 'target/*.jar'
  }

  stage('Static Code Analysis') {
    sh "'${mvnHome}/bin/mvn' clean verify sonar:sonar -Dsonar.projectName=example-project -Dsonar.projectKey=example-project -Dsonar.projectVersion=$BUILD_NUMBER";
}

  // stage ('Publish') {}
}
