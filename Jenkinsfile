pipeline {

  agent any
  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS = credentials('deploy-anypoint-user')
    MULE_VERSION = '4.3.0'
    BG = "ATT Product Day"
    WORKER = "Micro"
  }
  stages {
    stage('Build') {
      steps {
            mvn -B -U -e -V clean -DskipTests package
      }
    }

    stage('Test') {
      steps {
          mvn test
      }
    }

     stage('Deploy Development') {
      environment {
        ENVIRONMENT = 'Sandbox'
        APP_NAME = 'rtf-cicd-hello-world'
      }
      steps {
            mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.app="%APP_NAME%" -Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.bg="%BG%" -Dcloudhub.worker="%WORKER%"
      }
    }
  }

  tools {
    maven 'M3'
  }
}