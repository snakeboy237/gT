pipeline {
  agent any

  environment {
    TAG_NAME = ''
    CLIENT = ''
    DEPLOY_ENV = ''
  }

  stages {
    stage('Detect Tag') {
      when {
        expression { return env.GIT_BRANCH?.startsWith("refs/tags/") }
      }
      steps {
        script {
          TAG_NAME = env.GIT_BRANCH.replace("refs/tags/", "")
          echo "Building from tag: ${TAG_NAME}"

         
          def parts = TAG_NAME.tokenize('-')
          if (parts.size() == 4) {
            CLIENT = "${parts[1]}-${parts[2]}"
            DEPLOY_ENV = parts[3]
            
          } else {
            error "Invalid tag format. Use deploy-client-a-prod"
          }

          echo "Client: ${CLIENT}"
          echo "Environment: ${DEPLOY_ENV}"
        }
      }
    }

    stage('Deploy') {
      when {
        expression { return CLIENT && DEPLOY_ENV }
      }
      steps {
        echo "🚀 Deploying ${CLIENT} to ${DEPLOY_ENV}"
        // insert deployment logic here
      }
    }
  }
}
