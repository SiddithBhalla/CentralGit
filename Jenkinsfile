pipeline {
  agent any
  
  environment {
  ANYPOINT = ('anypoint_creds')
  }
  
  stages {
    stage('Build') {
      steps {
            bat 'mvn -B -U -e -V clean -DskipTests package'
      }
    }

    stage('Test') {
      steps {
          echo "Skipping munits as it is not supported"
      }
    }

     stage('DeploymentToDev') {
      environment {
      CLIENT_ID = credentials('dev_client_id')
      CLIENT_SECRET = credentials('dev_client_secret')
      }
      steps {
            bat 'mvn -U -V -e -B -DskipTests -Pdev deploy -DmuleDeploy -Dusername="%ANYPOINT_USR%" -Dpassword="%ANYPOINT_PSW%" -Ddev.anypoint.platform.client_id="%CLIENT_ID%" -Ddev.anypoint.platform.client_secret="%CLIENT_SECRET%"'
      }  
    }
    stage('DeploymentToSandbox') {
      environment {
      sandbox_client_id = credentials('sandbox_client_id')
      sandbox_client_secret = credentials('sandbox_client_secret')
      }
      steps {
            bat 'mvn -U -V -e -B -DskipTests -PSandbox deploy -DmuleDeploy  -Dusername="%anypoint_creds_USR%" -Dpassword="%anypoint_creds_PSW%" -Dsandbox.anypoint.platform.client_id="%sandbox_client_id%" -Dsandbox.anypoint.platform.client_secret="%sandbox_client_secret%"'
      }  
    }
  }
}