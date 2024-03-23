 pipeline {
  agent any
  //tools {
  //   maven 'Maven'
  //}
  parameters {
     string(name: 'VERSION', defaultValue: '', description: 'Version to deploy')
     choice(name: 'ENV', choices: ['VF', 'HF', 'PROD'], description: 'Environment')
     booleanParam(name: 'executeTests', defaultValue: true, description: 'launch tests ?')
  }
  environment {
    CODE_CHANGES = 'true'
    CREDENTIALS = credentials('erabot-password')
  }
  stages {
    stage('init') {
     steps {
      script {
          gv = load "script.groovy"
      }
     }
    }
    stage('build') {
      when {
        expression {
          CODE_CHANGES.toBoolean()
        }
      }
      steps {
        echo "Building ${JOB_NAME}.${BUILD_ID} for ${params.VERSION}"
        gv.aFunction()
        sh "mvn --version" 
      }
    }
    stage('test') {
      when {
        expression {
          (BRANCH_NAME == 'dev' || BRANCH_NAME == 'main') && params.executeTests
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
        echo "Deploying ${params.ENV}"
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
