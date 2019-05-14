#!groovy

node('master') {
  stage('Checkout') {
    checkout scm
  }
    
  stage('Run tests') {
    try {
      withMaven(maven: 'Maven 3.3.3', mavenSettingsConfig: 'bc30ebe0-68e1-4fa7-ab30-38092113a63c') {
        dir('bobcat') {
          sh 'mvn clean test -Dwebdriver.type=remote -Dwebdriver.url=http://172.21.0.7:4445/wd/hub -Dwebdriver.cap.browserName=chrome -Dmaven.test.failure.ignore=true'
          sh 'mvn clean test -Dwebdriver.type=remote -Dwebdriver.url=http://172.21.0.7:4445/wd/hub -Dwebdriver.cap.browserName=firefox -Dmaven.test.failure.ignore=true'
        }
      }
    } finally {
      junit testResults: 'bobcat/target/*.xml', allowEmptyResults: true
      archiveArtifacts 'bobcat/target/**'
    }
  }
}
