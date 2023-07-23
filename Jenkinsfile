pipeline {
    triggers {
        pollSCM('H/5 * * * *')
    }
    agent {
      kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        metadata:
          labels:
            some-label: some-label-value
        spec:
          containers:
          - name: python
            image: nctiggy/python-build-image
            command:
            - sleep
            args:
            - 99d
        '''
      }
    }

    environment {
        TEST_PREFIX = "test-IMAGE"
        TEST_IMAGE = "${env.TEST_PREFIX}:${env.BUILD_NUMBER}"
        TEST_CONTAINER = "${env.TEST_PREFIX}-${env.BUILD_NUMBER}"
        COVERALLS_TOKEN = credentials("coverallsToken")
    }

    stages {
        stage("something always do") {
            steps {
            container('python') {
                sh """
                    ls -ltra
                    git rev-parse --abbrev-ref HEAD
                    printenv
                    python --version
                """
            }
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
