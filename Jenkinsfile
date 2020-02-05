pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/chrisms91/GitTest.git'
      }
    }

    stage('Restore Nuget Package') {
      steps {
        bat 'C:\\\\nuget.exe restore "%WORKSPACE%\\\\GitTest.sln'
      }
    }

    stage('Build') {
      steps {
        bat 'C:\\\\Program Files (x86)\\\\Microsoft Visual Studio\\\\2017\\\\Professional\\\\MSBuild\\\\15.0\\\\Bin\\\\MSBuild.exe" GitTest.sln /p:Configuration=Debug /p:Platform="Any CPU'
      }
    }

  }
}