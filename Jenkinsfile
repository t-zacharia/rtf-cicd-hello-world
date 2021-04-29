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
            sh 'mvn -f pom.xml -B -U -e -V clean -DskipTests package'
      }
    }

    stage('Test') {
      steps {
          sh "mvn -f pom.xml test"
      }
    }

    stage('Publish to Exchange') {
      steps {
         sh "mvn deploy"
      }
    }

     stage('Deploy Development') {
      environment {
        ENVIRONMENT = 'Sandbox'
        APP_NAME = 'rtf-cicd-hello-world'
      }
      steps {
            sh 'mvn -f pom.xml -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version="$MULE_VERSION" -Danypoint.username="$DEPLOY_CREDS_USR" -Danypoint.password="$DEPLOY_CREDS_PSW" -Drtf.app="$APP_NAME" -Drtf.environment="$ENVIRONMENT" -Drtf.bg="$BG"'
      }
    }
  }

//  tools {
//    maven 'M3'
//  }
}