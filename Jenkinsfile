pipeline {
  agent any
  }
  environment {
    GIT_COMMIT = getCommit()
    dir = pwd()
  }
  stages {
    stage('env') {
      agent any
      steps {
        echo sh(returnStdout: true, script: 'env')
        sh "echo ${currentBuild.buildCauses}"
      }
    }
    stage('Init') {
      agent any
      steps {
        echo 'Init Stage'
      }
    }
    stage('Main Pipeline') {
      parallel {
        stage('Testing') {
          agent any
          steps {
            echo 'Testing Stage'
          }
        }
        stage('build') {
          agent any
          steps {
            echo 'Build Stage'
          }
        }
      }
    }
    stage('publish') {
      steps {
        echo 'Publish Stage'
      }
    }

  post {
    always {
      deleteDir()

    }

    success {
      echo "SUCCESS: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})"

    }

    unstable {
      echo "UNSTABLE: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})"

    }

    failure {
      echo "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})"

    }

  }
}
