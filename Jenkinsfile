pipeline {
    triggers {
        pollSCM('H/5 * * * *')
    }
    agent {
      kubernetes {
        containerTemplate {
            name 'python'
            image 'nctiggy/python-build-image'
            command 'cat'
        }
      }
    }

    environment {
        TEST_PREFIX = "test-IMAGE"
        TEST_IMAGE = "${env.TEST_PREFIX}:${env.BUILD_NUMBER}"
        TEST_CONTAINER = "${env.TEST_PREFIX}-${env.BUILD_NUMBER}"
        COVERALLS_TOKEN = credentials("coverallsToken")
    }

    stages {
        stage("something on push") {
            steps {
                sh "ls -ltra"
                sh "git rev-parse --abbrev-ref HEAD"
                sh "printenv"
            }
        }
        stage("something on tag") {
            when {
                buildingTag()
            }
            steps {
                sh "ls -ltra"
                sh "git rev-parse --abbrev-ref HEAD"
                sh "printenv"
            }
        }
    }
}
