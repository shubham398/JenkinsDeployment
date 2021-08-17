pipeline {
  agent any
  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS = credentials('86d51786-97f1-4fb7-9930-783d9ea2df06')
    MULE_VERSION = '4.3.0'
    BG = "Apisro"
    WORKER = "Micro"
  }
  stages {
    stage('Build') {
      steps {
            bat 'mvn -B -U -e -V clean -DskipTests package',
			properties([parameters([string(defaultValue: 'ANYPOINT', description: 'DEPLOYMENT URL', name: 'ANYPOINT_URI')])])
      }
    }
     stage('Deploy Development') {
      environment {
        ENVIRONMENT = ''
        APP_NAME = ''
      }
      steps {
             bat 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Danypoint.uri="https://anypoint.mulesoft.com" -Dmule.version="4.3.0" -Danypoint.username="shubham06011997" -Danypoint.password="Shubhb@j1997" -Dcloudhub.app="CICDJenkinsTrial0601" -Dcloudhub.environment="Sandbox" -Dcloudhub.bg="Apisro" -Dcloudhub.worker="Micro" -Dcloudhub.region="us-east-1"'
      }
    }
  }
}