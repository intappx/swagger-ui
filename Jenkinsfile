def buildLog = "build.log"
def jenkinsCredentialsId = "6b7a2a4e-831b-4713-bcdd-736d23cc6b53"
def jenkinsAccountName = "jenkinsintapp"
def artifactoryCredentialsId = "artifacts.intappx.com"

pipeline {
  agent {
    label 'ubuntu2'
  }

  parameters {
    booleanParam(
      name: 'PRODUCTION',
      defaultValue: false,
      description: 'Is production deployment?'
    )
  }

  stages {
    stage("Prepare Environment") {
      steps {
        sh "printenv"
        sh "echo ${env.GIT_BRANCH}"
        sh "sudo rm -rf node_modules"
        sh "npm install > $buildLog 2>&1"
      }
    }

    stage("Build application") {
      steps {
        script {
          try {
            sh "npm run build > $buildLog 2>&1"
          } finally {
            archiveArtifacts "$buildLog"
          }
        }
      }
    }
  }
}
