pipeline {
  agent any
  stages {
    stage('Parallel Execution') {
      stage('clown down') {
          steps {
            stash excludes: '.git', name: 'code'
          }
      }
      parallel {
        stage('Say hello') {
          steps {
            sh 'echo "hello world"'
          }
        }

        stage('Build app') {
          agent {
            docker {
              image 'gradle:jdk11'
            }

          }
          steps {
            sh 'ci/build-app.sh'
            archiveArtifacts 'app/build/libs/'
          }
        }

      }
    }

  }
}
