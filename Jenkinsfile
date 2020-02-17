pipeline {
  agent none
  stages {
    stage('Checking out') {
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
        stage ('Deploy to dev') {
          when {
            branch 'development'
          }
          steps {
            echo 'Developement Branch is deployed to dev server'
          }
        }
      }
    }

    // stage('Deploy') {
    //   agent none
    //   input {
    //     message "Should we deploy to dev?"
    //     ok "Deploy"
    //   }
    //   steps {
    //     echo "Deploying..."
    //   }
    // }

  }
} 