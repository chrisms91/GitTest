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
        bat '"\\"${tool \'MSBuild 2017\'}\\" GitTest.sln /p:Configuration=Debug /p:Platform=\\"Any CPU\\""'
      }
    }

  }
}