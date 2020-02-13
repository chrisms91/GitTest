pipeline {
  agent none
  stages {
    stage('Restore Nuget Package and Build Project') {
      agent { label 'master'}
      stages {
        stage ('Restore Nuget Package') {
          steps {
            bat 'C:\\\\nuget.exe restore "%WORKSPACE%\\\\GitTest.sln'
          }
        }
        stage ('Build Project') {
          steps {
            bat 'C:\\\\Progra~2\\\\Micros~2\\\\2017\\\\Professional\\\\MSBuild\\\\15.0\\\\Bin\\\\MSBuild.exe GitTest.sln -verbosity:diagnostic /p:Configuration=Debug /p:Platform="Any CPU"'
          }
        }
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

  }
} 