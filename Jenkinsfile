pipeline {
  agent any
  
  stages {
    stage('Build') {
      steps {
            bat 'mvn -B -U -e -V clean -gs %M2SETTINGS% -DskipTests package'
      }
    }

    stage('Test') {
      steps {
          echo "Skipping munits as it is not supported"
      }
    }

     stage('Deployment') {
      steps {
            bat 'mvn -U -V -e -B -DskipTests -Pdev deploy -DmuleDeploy"'
      }  
    }
  }
}