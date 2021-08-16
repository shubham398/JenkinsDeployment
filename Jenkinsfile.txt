pipeline {
  agent any
  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS = credentials('anypoint.devops.id')
    MULE_VERSION = '4.3.0'
    BG = "Apisro"
    WORKER = "Micro"
  }
  stages {
    stage('Build') {
      steps {
            sh 'source /etc/profile.d/maven.sh; mvn -B -U -e -V clean -DskipTests package'
      }
    }
     stage('Deploy Development') {
      environment {
        ENVIRONMENT = ''
        APP_NAME = ''
      }
      steps {
             mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Danypoint.uri="https://anypoint.mulesoft.com" -Dmule.version="4.3.0" -Danypoint.username="shubham06011997" -Danypoint.password="Shubhb@j1997" -Dcloudhub.app="CICDJenkinsTrial" -Dcloudhub.environment="Sandbox" -Dcloudhub.bg="Apisro" -Dcloudhub.worker="Micro" -Dcloudhub.region="us-east-1"'
      }
    }
  }
}