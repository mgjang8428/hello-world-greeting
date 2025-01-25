node ('built-in') {

  def mvnHome
  def sonarqubeHome

  stage('Preparation') {
    mvnHome = tool 'M3'
    sonarqubeHome = tool 'sonarqube-scanner'
  }
    
  stage('Poll') {
    checkout scm
  }
  
  stage('Build & Unit test') {
    sh "'${mvnHome}/bin/mvn' clean verify -DskipITs=true"
    junit '**/target/surefire-reports/TEST-*.xml'
    archive 'target/*.jar'
  }

  stage('Static Code Analysis') {
    sh "'${mvnHome}/bin/mvn' clean verify"
    withSonarQubeEnv(credentialsId: "sonarqube", installationName: 'sonarqube') {
      sh "'${sonarqubeHome}/bin/sonar-scanner' -Dsonar.projectName=example-project -Dsonar.projectKey=example-project -Dsonar.projectVersion=$BUILD_NUMBER";
    }
}

  stage ('Publish') {
    sh 'scp target/*.jar root@erms-ubuntu:/root'
  }
}
