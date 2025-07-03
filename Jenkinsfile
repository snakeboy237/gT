// Jenkins pipeline config
pipeline {
    agent any

    environment {
        CLIENT = ""
        DEPLOY_ENV = ""
    }

    stages {

        stage('Get tag') {
            when {
                expression { return env.GIT_TAG != null }
            }
        }
        steps {
            script {
                def tagParts = env.GIT_TAG.tokenize('-')
                if (tagParts.size() == 4) {
                    CLIENT = "${tagParts[0]}-${tagParts[1]}-${tagParts[2]}"
                    DEPLOY_ENV = "${tagParts[3]}"
                } else {
                    error "Check tag in Commit"
                }
                echo "Client: ${CLIENT}"
                echo "Deploy Environment: ${DEPLOY_ENV}"
            }
        }

        /*stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }*/

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