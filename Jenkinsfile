pipeline {
    agent { node { label 'kubeagent' } }

    environment {
        TEST_PREFIX = "test-IMAGE"
        TEST_IMAGE = "${env.TEST_PREFIX}:${env.BUILD_NUMBER}"
        TEST_CONTAINER = "${env.TEST_PREFIX}-${env.BUILD_NUMBER}"

        COVERALLS_TOKEN = credentials("coverallsToken")

    }

    stages {
        when {
            branch "main"
        }
        stage("something on push") {
            steps {
                sh "ls -ltra"
                sh "git describe"
                sh "printenv"
            }
        }
    }
}
