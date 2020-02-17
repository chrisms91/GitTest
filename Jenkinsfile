pipeline {
  agent none
  stages {
    stage('Restore Nuget Package and Build Project') {
      agent {label 'master'}
      stages {
        stage('Restore Nuget Package') {
          steps {
            bat 'C:\\\\nuget.exe restore "%WORKSPACE%\\\\GitTest.sln'
          }
        }
        stage('Build Project') {
          steps {
            bat 'C:\\\\Progra~2\\\\Micros~2\\\\2017\\\\Professional\\\\MSBuild\\\\15.0\\\\Bin\\\\MSBuild.exe GitTest.sln -verbosity:diagnostic /p:Configuration=Debug /p:Platform="Any CPU"'
          }
        }
      }
      post {
        success {
          echo 'I succeeeded!! might need to stash workplace for later usage..'
          // stash
        }
        failure {
          echo 'I failed :( might need to set up notification via email or webex'
          // notification email | webex
        }
      }
    }
    
    // only when feature branch is merged to development branch
    stage('Deploy to development server') {
      agent {label 'master'}
      when {
        branch 'development'
      }
      steps {
        echo 'Development branch is deployed to dev server'
      }
    }

    // only when development branch is merged to master branch.
    stage('Preprod deploy approval') {
      agent none
      when {
        branch 'master'
      }
      input {
        message "D"
      }
    }

    stage('Deploy to preprod server') {
      agent {label 'master'}
      when {
        branch 'master'
      }
      steps {
        echo 'Master branch is deployed to preprod server'
      }
    }
  }
} 