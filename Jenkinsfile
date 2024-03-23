 pipeline {
  agent any
  //tools {
  //   maven 'Maven'
  //}
  environment {
    CODE_CHANGES = 'true'
    CREDENTIALS = credentials('erabot-password')
  }
  stages {
    stage('build') {
      when {
        expression {
          CODE_CHANGES.toBoolean()
        }
      }
      steps {
        echo "Building ${JOB_NAME}.${BUILD_ID}"
        sh "mvn --version" 
      }
    }
    stage('test') {
      when {
        expression {
          BRANCH_NAME == 'dev' || BRANCH_NAME == 'main'
        }
      }
        steps {
          echo CODE_CHANGES
          echo BRANCH_NAME
          echo 'Testing'
        }
    }
    stage('deploy') {
      steps {
         withCredentials([usernamePassword(credentialsId: 'erabot-password', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
        	   sh "echo \"${USERNAME} ${PASSWORD}\""
        }
        echo 'Deploying'
      }
    }
  }
  post {
    always {
      echo 'always'
    }
    success {
      echo 'success'
    }
    failure {
      echo 'failure'
    }
  }
}
