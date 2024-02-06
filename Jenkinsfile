pipeline {
  agent none
  environment {
    DISABLE="SPELL"
    DISABLE_ERRORS=true
  }
  stages {
    stage('MegaLinter') {
      agent {
        docker {
            image 'oxsecurity/megalinter-cupcake:v7.8.0'
            args "-u root -e VALIDATE_ALL_CODEBASE=true -v \${WORKSPACE}:/tmp/lint --entrypoint=''"
            reuseNode true
        }
      }
      steps {
        sh '/entrypoint.sh'
      }
      post {
        always {
          archiveArtifacts(allowEmptyArchive: true, artifacts: 'mega-linter.log,,megalinter-reports/**/*', defaultExcludes: false, followSymlinks: false)
        }
      }
    }
  }
}
