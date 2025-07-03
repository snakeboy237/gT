pipeline {
  agent any

  triggers {
    // This only works for regular branches
    // Tags won't be triggered by this unless detected by a scan
  }

  environment {
    TAG_NAME = "${env.GIT_BRANCH}".replace('refs/tags/', '')
  }

  stages {
    stage('Tag Check') {
      when {
        expression { return env.GIT_BRANCH?.startsWith("refs/tags/") }
      }
      steps {
        echo "🔖 This is a tag build: ${env.GIT_BRANCH}"
        echo "Extracted tag: ${TAG_NAME}"

        script {
          if (!TAG_NAME.startsWith("deploy-")) {
            error "❌ Tag name does not follow deploy-* format. Aborting."
          }
        }
      }
    }

    stage('Deploy') {
      when {
        expression { return env.GIT_BRANCH?.startsWith("refs/tags/deploy-") }
      }
      steps {
        echo "🚀 Deploy logic triggered for tag: ${TAG_NAME}"
        // insert actual deploy logic
      }
    }
  }
}
