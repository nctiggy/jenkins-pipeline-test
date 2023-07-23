pipeline {
    agent { node { label 'kubeagent' } }

    environment {
        TEST_PREFIX = "test-IMAGE"
        TEST_IMAGE = "${env.TEST_PREFIX}:${env.BUILD_NUMBER}"
        TEST_CONTAINER = "${env.TEST_PREFIX}-${env.BUILD_NUMBER}"
        COVERALLS_TOKEN = credentials("coverallsToken")

    }

    stages {
        stage("something on push") {
            when {
                branch "main"
            }
            steps {
                sh "ls -ltra"
                sh "git rev-parse --abbrev-ref HEAD"
                sh "printenv"
            }
        }
    }
}
