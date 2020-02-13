pipeline {
  agent none
  stages {
    stage('Restore Nuget Package') {
      agent { label 'master'}
      steps {
        bat 'C:\\\\nuget.exe restore "%WORKSPACE%\\\\GitTest.sln'
      }
    }

     stage('Deploy to Dev') {
      agent none
      input {
        message "Should we deploy to dev?"
        ok "Deploy"
      }
      steps {
        echo "Deploying..."
      }
    }

    stage('Build') {
      agent {label 'master'}
      steps {
        bat 'C:\\\\Progra~2\\\\Micros~2\\\\2017\\\\Professional\\\\MSBuild\\\\15.0\\\\Bin\\\\MSBuild.exe GitTest.sln -verbosity:diagnostic /p:Configuration=Debug /p:Platform="Any CPU"'
      }
    }

  }
}