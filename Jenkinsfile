def projectName = 'GitTest'

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
    // only when development branch is pushed to master branch.
    stage('Preprod deploy approval') {
      agent none
      when {
        beforeInput true
        branch 'master'
      }
      input {
        message 'Deploy to preprod?????'
        ok 'Deploy'
      }
      steps {
        echo 'Approved'
      }
    }

    stage('Deployments') {
      agent {label 'master'}
      options {
        skipDefaultCheckout true
      }
      when {
        anyOf {branch 'master'; branch 'development'}
      }
      stages{
        // only when feature branch is pushed to development branch
        stage('Deploy to development') {
          when { 
            branch 'development'
          }
          steps {
            bat 'xcopy "%WORKSPACE%"\\\\\\\\*.* C:\\Work\\Deploy\\GitTest\\ /s'
          }
        }
        stage('Deploy to preprod server') {
          when {
            branch 'master'
          }
          steps {
            echo 'Master branch is deployed to preprod server'
          }
        }
      }
    }
  }
} 

// expression {
//   isPr = (env.BRANCH_NAME ==~ /PR-*([a-z0-9]*)/)
//   isTargetDev = env.CHANGE_TARGET == 'development'
//   echo "env.BRANCH_NAME: ${env.BRANCH_NAME}, env.CHANGE_TARGET: ${env.CHANGE_TARGET}, isPr: ${isPr}, isDev: ${isTargetDev}"
//   return isPr && isTargetDev
// }