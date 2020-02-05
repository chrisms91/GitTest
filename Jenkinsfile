pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        def scmVars = checkout scm
      }
    }

    stage('Restore Nuget Package') {
      steps {
        bat 'C:\\\\nuget.exe restore "%WORKSPACE%\\\\GitTest.sln'
      }
    }

    stage('Build') {
      steps {
        bat 'C:\\\\Progra~2\\\\Micros~2\\\\2017\\\\Professional\\\\MSBuild\\\\15.0\\\\Bin\\\\MSBuild.exe GitTest.sln /p:Configuration=Debug /p:Platform="Any CPU"'
      }
    }

  }
}