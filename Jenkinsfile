pipeline {
  agent any
  stages {
    stage('Parallel stuff') {
      parallel {
        stage('say test') {
          steps {
            echo 'Hello test!'
          }
        }

        stage('build app') {
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
